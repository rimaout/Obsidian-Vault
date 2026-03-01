---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2026-02-25T15:13
updated: 2026-03-01T17:10
---
## Codice

```c
#include <stdio.h>
#include <stdlib.h>
#include <math.h>
#include "energy_storms.h"

#define NUM_THREADS_PER_BLOCK 256

#include <cuda.h>
struct max_pos {
    float max;
    int pos;
};

__global__ void layerUpdateKernel(float* layer, int layer_size, int* d_posval, int num_impacts, float threshold) {
    int myID = blockIdx.x * blockDim.x + threadIdx.x;

    if (myID < layer_size) {

        float total_energy_to_add = layer[myID]; // Start with the current energy at this position (non fotto con i float)

        for (int j = 0; j < num_impacts; j++) {
            int position = d_posval[j*2];
            float energy = (float)d_posval[j*2+1] * 1000.0f / layer_size;

            int distance = abs(position - myID) + 1;
            float atenuacion = sqrtf((float)distance);
            float energy_k = energy / atenuacion;

            if (energy_k >= threshold || energy_k <= -threshold) {
                total_energy_to_add += energy_k;
            }
        }

        // Write to global memory ONLY ONCE at the end
        layer[myID] = total_energy_to_add;
    }
}

__global__ void layer_stancil_kernel(float* layer, float* layer_copy, int layer_size) {
    int myID = blockIdx.x * blockDim.x + threadIdx.x;

    if (myID > 0 && myID < layer_size - 1) {
        layer[myID] = (layer_copy[myID - 1] + layer_copy[myID] + layer_copy[myID + 1]) / 3.0f;
    }
}

__global__ void local_max_kernel(float* layer, struct max_pos* max_per_block, int layer_size) {
    int myID = blockIdx.x * blockDim.x + threadIdx.x;
    int local_thread_id = threadIdx.x;
    int block_size = blockDim.x;


    __shared__ struct max_pos local_max[NUM_THREADS_PER_BLOCK]; // Assuming blockDim.x <= 256

    local_max[local_thread_id].max = -INFINITY; // Initialize to negative infinity
    local_max[local_thread_id].pos = -1; // Initialize to invalid position

    if (myID < layer_size) {
        if (layer[myID] > local_max[local_thread_id].max) {
            local_max[local_thread_id].max = layer[myID];
            local_max[local_thread_id].pos = myID;
        }
    }

    __syncthreads();

    // Reduction to find the maximum in the block
    for (int offset = block_size / 2; offset > 0; offset /= 2) {
        if (local_thread_id < offset) {
            if (local_max[local_thread_id + offset].max > local_max[local_thread_id].max) {
                local_max[local_thread_id] = local_max[local_thread_id + offset];
            }
        }
        __syncthreads();
    }

    // The first thread in the block writes the block's maximum to global memory
    if (local_thread_id == 0) {
        max_per_block[blockIdx.x] = local_max[0];
    }
}

void core(int layer_size, int num_storms, Storm *storms, float *maximum, int *positions) {
    float threshold = THRESHOLD / layer_size;

    // - DEFINE DIMENSIONS
    int threadsPerBlock = NUM_THREADS_PER_BLOCK; 
    int blocksPerGrid = (layer_size + threadsPerBlock - 1) / threadsPerBlock; // Calculate blocks needed (ceil division)
    // - ALLOCATE HOST LAYER
    float *layer;
    cudaError_t err0 = cudaMallocHost((void**)&layer, layer_size * sizeof(float));
    if (err0 != cudaSuccess) {
        printf("CUDA Host Memory allocation error\n");
        return;
    }
    memset(layer, 0, layer_size * sizeof(float));

    // - ALLOCATE DEVICE LAYER
    float *d_layer, *d_layer_copy;
    cudaError_t err1 = cudaMalloc((void**)&d_layer,      sizeof(float) * layer_size);
    cudaError_t err2 = cudaMalloc((void**)&d_layer_copy, sizeof(float) * layer_size);
    if (err1 != cudaSuccess) {
        printf("CUDA Error allocating device layer: %s\n", cudaGetErrorString(err1));
        return;
    }
    if (err2 != cudaSuccess) {
        printf("CUDA Error allocating device layer copy: %s\n", cudaGetErrorString(err2));
        return;
    }

    // - POSVAL ARRAY ALLOCATION ON DEVICE
    int max_storm_size = 0;
    for(int i=0; i<num_storms; i++) { 
        if(storms[i].size > max_storm_size) max_storm_size = storms[i].size; 
    }
    int *d_posval;
    cudaError_t err3 = cudaMalloc((void**)&d_posval, max_storm_size * 2 * sizeof(int)); // * 2 sice each particle has position and energy 
    if (err3 != cudaSuccess) {
        printf("CUDA Error allocating device particles array: %s\n", cudaGetErrorString(err3));
        return;
    }
    
    struct max_pos *d_block_local_max;
    cudaError_t err4 = cudaMalloc((void**)&d_block_local_max, sizeof(struct max_pos) * blocksPerGrid);
    if (err4 != cudaSuccess) {
        printf("CUDA Error allocating device block local max array: %s\n", cudaGetErrorString(err4));
        return;
    }

    struct max_pos *h_block_local_max;
    cudaError_t err5 = cudaMallocHost((void**)&h_block_local_max, sizeof(struct max_pos) * blocksPerGrid);
    if (err5 != cudaSuccess) {
        printf("CUDA Host Memory allocation error for block local max: %s\n", cudaGetErrorString(err5));
        return;
    }

    // ------------------------------------------------------------------------------------------
    for( int i=0; i<num_storms; i++) {

        // - Move the layer to device
        //cudaMemcpy(d_layer, layer, sizeof(float) * layer_size, cudaMemcpyHostToDevice);
        
        // - Move the particles of the current storm to device
        cudaMemcpy(d_posval, storms[i].posval, sizeof(int) * storms[i].size * 2, cudaMemcpyHostToDevice);

        // - Update Layer
        layerUpdateKernel<<<blocksPerGrid, threadsPerBlock>>>(d_layer, layer_size, d_posval, storms[i].size, threshold);

        // Copy layer to layer_copy for the next step
        cudaMemcpy(d_layer_copy, d_layer, sizeof(float) * layer_size, cudaMemcpyDeviceToDevice);
        
        // - Apply stancil (smoothing - 3 points average)
        layer_stancil_kernel<<<blocksPerGrid, threadsPerBlock>>>(d_layer, d_layer_copy, layer_size);


        local_max_kernel<<<blocksPerGrid, threadsPerBlock>>>(d_layer, d_block_local_max, layer_size);

        // - Copy back the updated layer to host
        cudaDeviceSynchronize();
        cudaMemcpy(h_block_local_max, d_block_local_max, sizeof(struct max_pos) * blocksPerGrid, cudaMemcpyDeviceToHost);
        //cudaMemcpy(layer, d_layer, sizeof(float) * layer_size, cudaMemcpyDeviceToHost); // copy back to host
        
        // ------------------------------------------------------------------------------------------
        struct max_pos global_max;
        global_max.max = h_block_local_max[0].max;
        global_max.pos = h_block_local_max[0].pos;
        for( int k=1; k<blocksPerGrid; k++ ) {
            if (h_block_local_max[k].max > global_max.max) {
                global_max.max = h_block_local_max[k].max;
                global_max.pos = h_block_local_max[k].pos;
            }
        }

        maximum[i] = global_max.max;
        positions[i] = global_max.pos;
        /* 4.3. Locate the maximum value in the layer, and its position 
        for( int k=1; k<layer_size-1; k++ ) {
            // Check it only if it is a local maximum 
            if ( layer[k] > layer[k-1] && layer[k] > layer[k+1] ) {
                if ( layer[k] > maximum[i] ) {
                    maximum[i] = layer[k];
                    positions[i] = k;
                }
            }
        }
        */
    }

    // Cleanup
    cudaFree(d_layer);
    cudaFree(d_layer_copy);
    cudaFree(d_posval);
    cudaFreeHost(layer);
}
```

## Modifiche Fatte

- aggiunto kernel per parallelizzare la ricerca del massimo
- questo permette di non dover spostare tutto il layer dalla gpu alla cpu ma soltanto una sua riduzione (che per ora è un 256 esimo del layer) 
  
TODO:
- Fai una altra riduzione in modo tale da mandare il sislutato comleto alla cpu (un solo pos e val) infatti su i test da 100 milioni di elementi la il layer ottenuto dalla riduzione del massimo è comunque molto gramde (fatto in [[Cuda v5]] )
- usa `__constant__` per tutti i puntatori a costanti

## Risultati

**TEST1 Simulation:**

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_01_a35_p8_w1 test_files/test_01_a35_p7_w2 test_files/test_01_a35_p5_w3 test_files/test_01_a35_p8_w4

Time: 0.003735
Result: 14 19098.357422 14 24859.306641 10 30043.429688 3 54815.644531
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_01_a35_p8_w1 test_files/test_01_a35_p7_w2 test_files/test_01_a35_p5_w3 test_files/test_01_a35_p8_w4

Time: 0.003241
Result: 14 19098.357422 14 24859.306641 10 30043.429688 3 54815.644531
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_01_a35_p8_w1 test_files/test_01_a35_p7_w2 test_files/test_01_a35_p5_w3 test_files/test_01_a35_p8_w4

Time: 0.003199
Result: 14 19098.357422 14 24859.306641 10 30043.429688 3 54815.644531
```

**TEST2 Simulation:**

```c
srun -N 1 -n 1 ./energy_storms_cuda 20000 test_files/test_02_a30k_p20k_w1 test_files/test_02_a30k_p20k_w2 test_files/test_02_a30k_p20k_w3 test_files/test_02_a30k_p20k_w4 test_files/test_02_a30k_p20k_w5 test_files/test_02_a30k_p20k_w6

Time: 0.035445
Result: 17197 1654.755371 17223 3274.642578 17229 5727.363281 17222 8155.511230 15849 11403.597656 15924 14647.188477
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20000 test_files/test_02_a30k_p20k_w1 test_files/test_02_a30k_p20k_w2 test_files/test_02_a30k_p20k_w3 test_files/test_02_a30k_p20k_w4 test_files/test_02_a30k_p20k_w5 test_files/test_02_a30k_p20k_w6

Time: 0.035858
Result: 17197 1654.755371 17223 3274.642578 17229 5727.363281 17222 8155.511230 15849 11403.597656 15924 14647.188477
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20000 test_files/test_02_a30k_p20k_w1 test_files/test_02_a30k_p20k_w2 test_files/test_02_a30k_p20k_w3 test_files/test_02_a30k_p20k_w4 test_files/test_02_a30k_p20k_w5 test_files/test_02_a30k_p20k_w6

Time: 0.035422
Result: 17197 1654.755371 17223 3274.642578 17229 5727.363281 17222 8155.511230 15849 11403.597656 15924 14647.188477
```

**TEST3 Simulation:**

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_03_a20_p4_w1

Time: 0.003129
Result: 10 12966.631836
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_03_a20_p4_w1

Time: 0.003093
Result: 10 12966.631836
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_03_a20_p4_w1

Time: 0.003080
Result: 10 12966.631836
```

**TEST4 Simulation:**

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_04_a20_p4_w1

Time: 0.003141
Result: 16 12966.632812
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_04_a20_p4_w1

Time: 0.003101
Result: 16 12966.632812
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_04_a20_p4_w1

Time: 0.003091
Result: 16 12966.632812
```

**TEST5 Simulation:**

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_05_a20_p4_w1

Time: 0.003111
Result: 9 12829.288086
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_05_a20_p4_w1

Time: 0.003128
Result: 9 12829.288086
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_05_a20_p4_w1

Time: 0.003143
Result: 9 12829.288086
```

**TEST6 Simulation:**

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_06_a20_p4_w1

Time: 0.003106
Result: 16 12829.288086
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_06_a20_p4_w1

Time: 0.003156
Result: 16 12829.288086
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_06_a20_p4_w1

Time: 0.003133
Result: 16 12829.288086
```

**TEST7 Simulation:**

```c
srun -N 1 -n 1 ./energy_storms_cuda 1000000 test_files/test_07_a1M_p5k_w1 test_files/test_07_a1M_p5k_w2 test_files/test_07_a1M_p5k_w3 test_files/test_07_a1M_p5k_w4

Time: 0.111588
Result: 507805 12177.071289 400548 23157.615234 511786 34230.769531 511786 44824.339844
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 1000000 test_files/test_07_a1M_p5k_w1 test_files/test_07_a1M_p5k_w2 test_files/test_07_a1M_p5k_w3 test_files/test_07_a1M_p5k_w4

Time: 0.090334
Result: 507805 12177.071289 400548 23157.615234 511786 34230.769531 511786 44824.339844
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 1000000 test_files/test_07_a1M_p5k_w1 test_files/test_07_a1M_p5k_w2 test_files/test_07_a1M_p5k_w3 test_files/test_07_a1M_p5k_w4

Time: 0.090290
Result: 507805 12177.071289 400548 23157.615234 511786 34230.769531 511786 44824.339844
```
