---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2026-03-01T22:35
updated: 2026-03-01T22:44
---
## Codice

```c
#include <stdio.h>
#include <stdlib.h>
#include <math.h>
#include <cuda.h>

#include "energy_storms.h"

#define NUM_THREADS_PER_BLOCK 256

struct max_pos {
    float max;
    int pos;
};

__global__ void layerUpdateKernel(float* layer, int layer_size, int* d_posval, int num_impacts, float threshold, float energy_scale) {
    int myID = blockIdx.x * blockDim.x + threadIdx.x;

    if (myID < layer_size) {
        float total_energy_to_add = layer[myID];    // use register to accumulate energy

        for (int j = 0; j < num_impacts; j++) {
            int position = d_posval[j*2];
            float energy = (float)d_posval[j*2+1] * energy_scale;

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

__global__ void max_reduction_kernel(struct max_pos* data, int size) {
    int myID = blockIdx.x * blockDim.x + threadIdx.x;
    int local_thread_id = threadIdx.x;
    int block_size = blockDim.x;

    __shared__ struct max_pos local_max[NUM_THREADS_PER_BLOCK];

    local_max[local_thread_id].max = -INFINITY;
    local_max[local_thread_id].pos = -1;

    if (myID < size) {
        local_max[local_thread_id] = data[myID];
    }

    __syncthreads();

    for (int offset = block_size / 2; offset > 0; offset /= 2) {
        if (local_thread_id < offset && (myID + offset) < size) {
            if (local_max[local_thread_id + offset].max > local_max[local_thread_id].max) {
                local_max[local_thread_id] = local_max[local_thread_id + offset];
            }
        }
        __syncthreads();
    }

    if (local_thread_id == 0) {
        data[blockIdx.x] = local_max[0];
    }
}

void core(int layer_size, int num_storms, Storm *storms, float *maximum, int *positions) {
    float threshold = THRESHOLD / (float)layer_size;
    float energy_scale = 1000.0f / (float)layer_size;

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
    
    // - Allocate array for block local maxima
    struct max_pos *d_block_local_max;
    cudaError_t err4 = cudaMalloc((void**)&d_block_local_max, sizeof(struct max_pos) * blocksPerGrid);
    if (err4 != cudaSuccess) {
        printf("CUDA Error allocating device block local max array: %s\n", cudaGetErrorString(err4));
        return;
    }

    // ------------------------------------------------------------------------------------------
    for( int i=0; i<num_storms; i++) {
        
        // - Move the particles of the current storm to device
        cudaMemcpy(d_posval, storms[i].posval, sizeof(int) * storms[i].size * 2, cudaMemcpyHostToDevice);

        // - Update Layer
        layerUpdateKernel<<<blocksPerGrid, threadsPerBlock>>>(d_layer, layer_size, d_posval, storms[i].size, threshold, energy_scale);

        // Copy layer to layer_copy for the next step
        cudaMemcpy(d_layer_copy, d_layer, sizeof(float) * layer_size, cudaMemcpyDeviceToDevice);
        
        // - Apply stancil (smoothing - 3 points average)
        layer_stancil_kernel<<<blocksPerGrid, threadsPerBlock>>>(d_layer, d_layer_copy, layer_size);


        // - FIND MAXIMUM VALUE AND POSITION
        int blocks = blocksPerGrid;
        int blocks_prev = blocks;
        local_max_kernel<<<blocks, threadsPerBlock>>>(d_layer, d_block_local_max, layer_size);
    
        while (blocks > 1) {            
            blocks_prev = blocks;
            blocks = (blocks_prev + threadsPerBlock - 1) / threadsPerBlock;

            max_reduction_kernel<<<blocks, threadsPerBlock>>>(d_block_local_max, blocks_prev);            
        }        
    
        // Copy the final result (single element) back to host
        struct max_pos global_max;
        cudaMemcpy(&global_max, d_block_local_max, sizeof(struct max_pos), cudaMemcpyDeviceToHost);

        maximum[i] = global_max.max;
        positions[i] = global_max.pos;
    }

    // Cleanup
    cudaFree(d_layer);
    cudaFree(d_layer_copy);
    cudaFree(d_posval);
    cudaFree(d_block_local_max);
    cudaFreeHost(layer);
}
```

## Modifiche

introdotto `energy_scale` come parametro di `layerUpdateKernel`, questo permette di calcolare solo una volta `float energy_scale = 1000.0f / (float)layer_size;` e poi fare dentro `layerUpdateKernel`:
- `float energy = (float)d_posval[j*2+1] * 1000.0f / layer_size;`

Invece di:
- `float energy = (float)d_posval[j*2+1] * energy_scale;`

## Tempi

Questo ci ha fatto passare da 36 ms a 28 ms in test2


**TEST1 Simulation:**

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_01_a35_p8_w1 test_files/test_01_a35_p7_w2 test_files/test_01_a35_p5_w3 test_files/test_01_a35_p8_w4

Time: 0.004676
Result: 14 19098.357422 14 24859.306641 10 30043.429688 3 54815.644531
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_01_a35_p8_w1 test_files/test_01_a35_p7_w2 test_files/test_01_a35_p5_w3 test_files/test_01_a35_p8_w4

Time: 0.004433
Result: 14 19098.357422 14 24859.306641 10 30043.429688 3 54815.644531
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_01_a35_p8_w1 test_files/test_01_a35_p7_w2 test_files/test_01_a35_p5_w3 test_files/test_01_a35_p8_w4

Time: 0.004465
Result: 14 19098.357422 14 24859.306641 10 30043.429688 3 54815.644531
```

**TEST2 Simulation:**

```c
srun -N 1 -n 1 ./energy_storms_cuda 20000 test_files/test_02_a30k_p20k_w1 test_files/test_02_a30k_p20k_w2 test_files/test_02_a30k_p20k_w3 test_files/test_02_a30k_p20k_w4 test_files/test_02_a30k_p20k_w5 test_files/test_02_a30k_p20k_w6

Time: 0.028344
Result: 17197 1654.755371 17223 3274.642822 17229 5727.363770 17222 8155.511230 15849 11403.597656 15924 14647.188477
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20000 test_files/test_02_a30k_p20k_w1 test_files/test_02_a30k_p20k_w2 test_files/test_02_a30k_p20k_w3 test_files/test_02_a30k_p20k_w4 test_files/test_02_a30k_p20k_w5 test_files/test_02_a30k_p20k_w6

Time: 0.029412
Result: 17197 1654.755371 17223 3274.642822 17229 5727.363770 17222 8155.511230 15849 11403.597656 15924 14647.188477
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20000 test_files/test_02_a30k_p20k_w1 test_files/test_02_a30k_p20k_w2 test_files/test_02_a30k_p20k_w3 test_files/test_02_a30k_p20k_w4 test_files/test_02_a30k_p20k_w5 test_files/test_02_a30k_p20k_w6

Time: 0.028379
Result: 17197 1654.755371 17223 3274.642822 17229 5727.363770 17222 8155.511230 15849 11403.597656 15924 14647.188477
```

**TEST3 Simulation:**

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_03_a20_p4_w1

Time: 0.004267
Result: 10 12966.631836
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_03_a20_p4_w1

Time: 0.004271
Result: 10 12966.631836
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_03_a20_p4_w1

Time: 0.004271
Result: 10 12966.631836
```

**TEST4 Simulation:**

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_04_a20_p4_w1

Time: 0.004307
Result: 16 12966.632812
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_04_a20_p4_w1

Time: 0.004368
Result: 16 12966.632812
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_04_a20_p4_w1

Time: 0.004290
Result: 16 12966.632812
```

**TEST5 Simulation:**

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_05_a20_p4_w1

Time: 0.004316
Result: 9 12829.288086
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_05_a20_p4_w1

Time: 0.004273
Result: 9 12829.288086
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_05_a20_p4_w1

Time: 0.004275
Result: 9 12829.288086
```

**TEST6 Simulation:**

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_06_a20_p4_w1

Time: 0.004288
Result: 16 12829.288086
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_06_a20_p4_w1

Time: 0.004309
Result: 16 12829.288086
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_06_a20_p4_w1

Time: 0.004280
Result: 16 12829.288086
```

**TEST7 Simulation:**

```c
srun -N 1 -n 1 ./energy_storms_cuda 1000000 test_files/test_07_a1M_p5k_w1 test_files/test_07_a1M_p5k_w2 test_files/test_07_a1M_p5k_w3 test_files/test_07_a1M_p5k_w4

Time: 0.082218
Result: 507805 12177.073242 400548 23157.617188 511786 34230.769531 511786 44824.339844
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 1000000 test_files/test_07_a1M_p5k_w1 test_files/test_07_a1M_p5k_w2 test_files/test_07_a1M_p5k_w3 test_files/test_07_a1M_p5k_w4

Time: 0.082324
Result: 507805 12177.073242 400548 23157.617188 511786 34230.769531 511786 44824.339844
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 1000000 test_files/test_07_a1M_p5k_w1 test_files/test_07_a1M_p5k_w2 test_files/test_07_a1M_p5k_w3 test_files/test_07_a1M_p5k_w4

Time: 0.082943
Result: 507805 12177.073242 400548 23157.617188 511786 34230.769531 511786 44824.339844
```

**TEST8 Simulation:**

```c
srun -N 1 -n 1 ./energy_storms_cuda 100000000 test_files/test_08_a100M_p1_w1 test_files/test_08_a100M_p1_w2 test_files/test_08_a100M_p1_w3

Time: 0.687022
Result: 10 0.000080 658423 0.000081 658423 0.000078
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 100000000 test_files/test_08_a100M_p1_w1 test_files/test_08_a100M_p1_w2 test_files/test_08_a100M_p1_w3

Time: 0.691336
Result: 10 0.000080 658423 0.000081 658423 0.000078
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 100000000 test_files/test_08_a100M_p1_w1 test_files/test_08_a100M_p1_w2 test_files/test_08_a100M_p1_w3

Time: 0.686913
Result: 10 0.000080 658423 0.000081 658423 0.000078
```

**TEST9 (16) Simulation:**

```c
srun -N 1 -n 1 ./energy_storms_cuda 16 test_files/test_09_a16-17_p3_w1

Time: 0.004398
Result: 15 241.892746
```

**TEST9 (17) Simulation:**

```c
srun -N 1 -n 1 ./energy_storms_cuda 17 test_files/test_09_a16-17_p3_w1

Time: 0.004343
Result: 15 193.299606
```

