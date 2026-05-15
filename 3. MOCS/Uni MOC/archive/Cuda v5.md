---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2026-03-01T15:57
updated: 2026-03-08T12:17
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
        layerUpdateKernel<<<blocksPerGrid, threadsPerBlock>>>(d_layer, layer_size, d_posval, storms[i].size, threshold);

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

## Modifiche Fatte

Fatto tutta la ricerca del massimo dentro la GPU, cosi da ridurre il peso della memoria da mandare dalla gpu alla cpu, prima (nella versione 4) era un 256esimo del layer ($\times 2$, dato che abbiamo un float e un int) ora è un solo elemento (un float e un int).

**Questo però non ha cambiato i tempi anche sui test con layer molto grandi.**

## Tempi

**TEST1 Simulation:**

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_01_a35_p8_w1 test_files/test_01_a35_p7_w2 test_files/test_01_a35_p5_w3 test_files/test_01_a35_p8_w4

Time: 0.004673
Result: 14 19098.357422 14 24859.306641 10 30043.429688 3 54815.644531
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_01_a35_p8_w1 test_files/test_01_a35_p7_w2 test_files/test_01_a35_p5_w3 test_files/test_01_a35_p8_w4

Time: 0.004602
Result: 14 19098.357422 14 24859.306641 10 30043.429688 3 54815.644531
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_01_a35_p8_w1 test_files/test_01_a35_p7_w2 test_files/test_01_a35_p5_w3 test_files/test_01_a35_p8_w4

Time: 0.004437
Result: 14 19098.357422 14 24859.306641 10 30043.429688 3 54815.644531
```

**TEST2 Simulation:**

```c
srun -N 1 -n 1 ./energy_storms_cuda 20000 test_files/test_02_a30k_p20k_w1 test_files/test_02_a30k_p20k_w2 test_files/test_02_a30k_p20k_w3 test_files/test_02_a30k_p20k_w4 test_files/test_02_a30k_p20k_w5 test_files/test_02_a30k_p20k_w6

Time: 0.036671
Result: 17197 1654.755371 17223 3274.642578 17229 5727.363281 17222 8155.511230 15849 11403.597656 15924 14647.188477
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20000 test_files/test_02_a30k_p20k_w1 test_files/test_02_a30k_p20k_w2 test_files/test_02_a30k_p20k_w3 test_files/test_02_a30k_p20k_w4 test_files/test_02_a30k_p20k_w5 test_files/test_02_a30k_p20k_w6

Time: 0.036766
Result: 17197 1654.755371 17223 3274.642578 17229 5727.363281 17222 8155.511230 15849 11403.597656 15924 14647.188477
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20000 test_files/test_02_a30k_p20k_w1 test_files/test_02_a30k_p20k_w2 test_files/test_02_a30k_p20k_w3 test_files/test_02_a30k_p20k_w4 test_files/test_02_a30k_p20k_w5 test_files/test_02_a30k_p20k_w6

Time: 0.037841
Result: 17197 1654.755371 17223 3274.642578 17229 5727.363281 17222 8155.511230 15849 11403.597656 15924 14647.188477
```

**TEST3 Simulation:**

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_03_a20_p4_w1

Time: 0.004469
Result: 10 12966.631836
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_03_a20_p4_w1

Time: 0.004449
Result: 10 12966.631836
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_03_a20_p4_w1

Time: 0.004406
Result: 10 12966.631836
```

**TEST4 Simulation:**

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_04_a20_p4_w1

Time: 0.004469
Result: 16 12966.632812
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_04_a20_p4_w1

Time: 0.004458
Result: 16 12966.632812
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_04_a20_p4_w1

Time: 0.004375
Result: 16 12966.632812
```

**TEST5 Simulation:**

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_05_a20_p4_w1

Time: 0.004414
Result: 9 12829.288086
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_05_a20_p4_w1

Time: 0.004328
Result: 9 12829.288086
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_05_a20_p4_w1

Time: 0.004309
Result: 9 12829.288086
```

**TEST6 Simulation:**

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_06_a20_p4_w1

Time: 0.004440
Result: 16 12829.288086
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_06_a20_p4_w1

Time: 0.004427
Result: 16 12829.288086
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 20 test_files/test_06_a20_p4_w1

Time: 0.004438
Result: 16 12829.288086
```

**TEST7 Simulation:**

```c
srun -N 1 -n 1 ./energy_storms_cuda 1000000 test_files/test_07_a1M_p5k_w1 test_files/test_07_a1M_p5k_w2 test_files/test_07_a1M_p5k_w3 test_files/test_07_a1M_p5k_w4

Time: 0.107805
Result: 507805 12177.071289 400548 23157.615234 511786 34230.769531 511786 44824.339844
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 1000000 test_files/test_07_a1M_p5k_w1 test_files/test_07_a1M_p5k_w2 test_files/test_07_a1M_p5k_w3 test_files/test_07_a1M_p5k_w4

Time: 0.087635
Result: 507805 12177.071289 400548 23157.615234 511786 34230.769531 511786 44824.339844
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 1000000 test_files/test_07_a1M_p5k_w1 test_files/test_07_a1M_p5k_w2 test_files/test_07_a1M_p5k_w3 test_files/test_07_a1M_p5k_w4

Time: 0.088140
Result: 507805 12177.071289 400548 23157.615234 511786 34230.769531 511786 44824.339844
```

**TEST8 Simulation:**

```c
srun -N 1 -n 1 ./energy_storms_cuda 100000000 test_files/test_08_a100M_p1_w1 test_files/test_08_a100M_p1_w2 test_files/test_08_a100M_p1_w3

Time: 0.700265
Result: 10 0.000080 658423 0.000081 658423 0.000078
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 100000000 test_files/test_08_a100M_p1_w1 test_files/test_08_a100M_p1_w2 test_files/test_08_a100M_p1_w3

Time: 0.697439
Result: 10 0.000080 658423 0.000081 658423 0.000078
```

```c
srun -N 1 -n 1 ./energy_storms_cuda 100000000 test_files/test_08_a100M_p1_w1 test_files/test_08_a100M_p1_w2 test_files/test_08_a100M_p1_w3

Time: 0.696588
Result: 10 0.000080 658423 0.000081 658423 0.000078
```

**TEST9 (16) Simulation:**

```c
srun -N 1 -n 1 ./energy_storms_cuda 16 test_files/test_09_a16-17_p3_w1

Time: 0.004445
Result: 15 241.892746
```

**TEST9 (17) Simulation:**

```c
srun -N 1 -n 1 ./energy_storms_cuda 17 test_files/test_09_a16-17_p3_w1

Time: 0.004492
Result: 15 193.299606
```

## Super Test
```
make run-tests-sequential
chmod +x run_all_tests_sequential.sh
./run_all_tests_sequential.sh 1 2 3 4 5 6 7 8 9 10
# Sequential run started
# Tests: 1 2 3 4 5 6 7 8 9 10
# Poll interval: 15s

==================================================
# Submitting test 1
# Submitted job id: 919132
# Waiting for job 919132 to leave queue...
# Job 919132 completed
# Parsing test_1_results_919132.raw
Parsing raw results from: test_1_results_919132.raw
size: 32         test: 1 mean: 0.003827 stddev: 0.000086 fails: 100.00%
size: 64         test: 1 mean: 0.003811 stddev: 0.000078 fails: 100.00%
size: 128        test: 1 mean: 0.003815 stddev: 0.000078 fails: 100.00%
size: 256        test: 1 mean: 0.003814 stddev: 0.000072 fails: 100.00%
size: 512        test: 1 mean: 0.003810 stddev: 0.000070 fails: 100.00%
size: 1024       test: 1 mean: 0.003810 stddev: 0.000071 fails: 100.00%

==================================================
# Submitting test 2
# Submitted job id: 919133
# Waiting for job 919133 to leave queue...
^Cmake: *** [Makefile:30: run-tests-sequential] Interrupt

ricchiuto_2134560@submitter:~/exam-waves/testing$ squeue
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
            919133  students cuda_wav ricchiut  R       0:41      1 node120
            919124  students last_los verde_20  R       5:06      1 node120
ricchiuto_2134560@submitter:~/exam-waves/testing$ squeue
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
            919124  students last_los verde_20  R       5:43      1 node120
ricchiuto_2134560@submitter:~/exam-waves/testing$ squeue
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
            919124  students last_los verde_20  R       5:44      1 node120
ricchiuto_2134560@submitter:~/exam-waves/testing$ make run-tests-sequential
chmod +x run_all_tests_sequential.sh
./run_all_tests_sequential.sh 1 2 3 4 5 6 7 8 9 10
# Sequential run started
# Tests: 1 2 3 4 5 6 7 8 9 10
# Poll interval: 15s

==================================================
# Submitting test 1
# Submitted job id: 919134
# Waiting for job 919134 to leave queue...
# Job 919134 completed
# Parsing test_1_results_919134.raw
Parsing raw results from: test_1_results_919134.raw
size: 32         test: 1 mean: 0.003832 stddev: 0.000086 fails: 0.00%
size: 64         test: 1 mean: 0.003808 stddev: 0.000077 fails: 0.00%
size: 128        test: 1 mean: 0.003815 stddev: 0.000071 fails: 0.00%
size: 256        test: 1 mean: 0.003796 stddev: 0.000083 fails: 0.00%
size: 512        test: 1 mean: 0.003819 stddev: 0.000078 fails: 0.00%
size: 1024       test: 1 mean: 0.003805 stddev: 0.000071 fails: 0.00%

==================================================
# Submitting test 2
# Submitted job id: 919135
# Waiting for job 919135 to leave queue...
# Job 919135 completed
# Parsing test_2_results_919135.raw
Parsing raw results from: test_2_results_919135.raw
size: 32         test: 2 mean: 0.027646 stddev: 0.001474 fails: 0.00%
size: 64         test: 2 mean: 0.027437 stddev: 0.000124 fails: 0.00%
size: 128        test: 2 mean: 0.028033 stddev: 0.000169 fails: 0.00%
size: 256        test: 2 mean: 0.029073 stddev: 0.000123 fails: 0.00%
size: 512        test: 2 mean: 0.029427 stddev: 0.000077 fails: 0.00%
size: 1024       test: 2 mean: 0.038906 stddev: 0.000164 fails: 0.00%

==================================================
# Submitting test 3
# Submitted job id: 919136
# Waiting for job 919136 to leave queue...
# Job 919136 completed
# Parsing test_3_results_919136.raw
Parsing raw results from: test_3_results_919136.raw
size: 32         test: 3 mean: 0.003701 stddev: 0.000085 fails: 0.00%
size: 64         test: 3 mean: 0.003726 stddev: 0.000077 fails: 0.00%
size: 128        test: 3 mean: 0.003707 stddev: 0.000071 fails: 0.00%
size: 256        test: 3 mean: 0.003709 stddev: 0.000075 fails: 0.00%
size: 512        test: 3 mean: 0.003703 stddev: 0.000094 fails: 0.00%
size: 1024       test: 3 mean: 0.003708 stddev: 0.000070 fails: 0.00%

==================================================
# Submitting test 4
# Submitted job id: 919137
# Waiting for job 919137 to leave queue...
# Job 919137 completed
# Parsing test_4_results_919137.raw
Parsing raw results from: test_4_results_919137.raw
size: 32         test: 4 mean: 0.003684 stddev: 0.000087 fails: 0.00%
size: 64         test: 4 mean: 0.003713 stddev: 0.000076 fails: 0.00%
size: 128        test: 4 mean: 0.003709 stddev: 0.000074 fails: 0.00%
size: 256        test: 4 mean: 0.003700 stddev: 0.000076 fails: 0.00%
size: 512        test: 4 mean: 0.003745 stddev: 0.000082 fails: 0.00%
size: 1024       test: 4 mean: 0.003721 stddev: 0.000072 fails: 0.00%

==================================================
# Submitting test 5
# Submitted job id: 919138
# Waiting for job 919138 to leave queue...
# Job 919138 completed
# Parsing test_5_results_919138.raw
Parsing raw results from: test_5_results_919138.raw
size: 32         test: 5 mean: 0.003705 stddev: 0.000089 fails: 0.00%
size: 64         test: 5 mean: 0.003697 stddev: 0.000073 fails: 0.00%
size: 128        test: 5 mean: 0.003712 stddev: 0.000070 fails: 0.00%
size: 256        test: 5 mean: 0.003707 stddev: 0.000112 fails: 0.00%
size: 512        test: 5 mean: 0.003703 stddev: 0.000083 fails: 0.00%
size: 1024       test: 5 mean: 0.003713 stddev: 0.000074 fails: 0.00%

==================================================
# Submitting test 6
# Submitted job id: 919139
# Waiting for job 919139 to leave queue...
# Job 919139 completed
# Parsing test_6_results_919139.raw
Parsing raw results from: test_6_results_919139.raw
size: 32         test: 6 mean: 0.003704 stddev: 0.000088 fails: 0.00%
size: 64         test: 6 mean: 0.003698 stddev: 0.000071 fails: 0.00%
size: 128        test: 6 mean: 0.003689 stddev: 0.000069 fails: 0.00%
size: 256        test: 6 mean: 0.003684 stddev: 0.000070 fails: 0.00%
size: 512        test: 6 mean: 0.003707 stddev: 0.000068 fails: 0.00%
size: 1024       test: 6 mean: 0.003698 stddev: 0.000072 fails: 0.00%

==================================================
# Submitting test 7
# Submitted job id: 919140
# Waiting for job 919140 to leave queue...
# Job 919140 completed
# Parsing test_7_results_919140.raw
Parsing raw results from: test_7_results_919140.raw
size: 32         test: 7 mean: 0.112191 stddev: 0.003780 fails: 0.00%
size: 64         test: 7 mean: 0.086424 stddev: 0.000294 fails: 0.00%
size: 128        test: 7 mean: 0.085678 stddev: 0.000992 fails: 0.00%
size: 256        test: 7 mean: 0.086102 stddev: 0.000234 fails: 0.00%
size: 512        test: 7 mean: 0.087346 stddev: 0.000368 fails: 0.00%
size: 1024       test: 7 mean: 0.119114 stddev: 0.312465 fails: 0.00%

==================================================
# Submitting test 8
# Submitted job id: 919141
# Waiting for job 919141 to leave queue...
# Job 919141 completed
# Parsing test_8_results_919141.raw
Parsing raw results from: test_8_results_919141.raw
size: 32         test: 8 mean: 0.739623 stddev: 0.018428 fails: 0.00%
size: 64         test: 8 mean: 0.742372 stddev: 0.018712 fails: 0.00%
size: 128        test: 8 mean: 0.739914 stddev: 0.020038 fails: 0.00%
size: 256        test: 8 mean: 0.741508 stddev: 0.022210 fails: 0.00%
size: 512        test: 8 mean: 0.741082 stddev: 0.017994 fails: 0.00%
size: 1024       test: 8 mean: 0.751162 stddev: 0.022866 fails: 0.00%

==================================================
# Submitting test 9
# Submitted job id: 919143
# Waiting for job 919143 to leave queue...
# Job 919143 completed
# Parsing test_9_results_919143.raw
Parsing raw results from: test_9_results_919143.raw
size: 32         test: 9 mean: 0.003729 stddev: 0.000093 fails: 100.00%
size: 64         test: 9 mean: 0.003717 stddev: 0.000079 fails: 100.00%
size: 128        test: 9 mean: 0.003721 stddev: 0.000074 fails: 100.00%
size: 256        test: 9 mean: 0.003755 stddev: 0.000074 fails: 100.00%
size: 512        test: 9 mean: 0.003735 stddev: 0.000075 fails: 100.00%
size: 1024       test: 9 mean: 0.003730 stddev: 0.000077 fails: 100.00%

==================================================
# Submitting test 10
# Submitted job id: 919144
# Waiting for job 919144 to leave queue...
# Job 919144 completed
# Parsing test_10_results_919144.raw
Parsing raw results from: test_10_results_919144.raw
size: 32         test: 10 mean: 0.003759 stddev: 0.000090 fails: 0.00%
size: 64         test: 10 mean: 0.003719 stddev: 0.000086 fails: 0.00%
size: 128        test: 10 mean: 0.003716 stddev: 0.000077 fails: 0.00%
size: 256        test: 10 mean: 0.003817 stddev: 0.000097 fails: 0.00%
size: 512        test: 10 mean: 0.003738 stddev: 0.000075 fails: 0.00%
size: 1024       test: 10 mean: 0.003812 stddev: 0.000085 fails: 0.00%

# Sequential run finished
```