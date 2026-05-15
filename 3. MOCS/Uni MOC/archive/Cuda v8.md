---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2026-03-03T16:17
updated: 2026-03-03T16:24
---
## Codice

```c
#include <stdio.h>
#include <stdlib.h>
#include <math.h>
#include <cuda.h>

#include "energy_storms.h"

#define NUM_THREADS_PER_BLOCK 256
#define SHARED_TILE_SIZE 1024 // 1 KB in bytes

struct Particle {
    int position;
    int energy;
};

struct max_pos {
    float max;
    int pos;
};

#define MAX_PARTICLES_PER_TILE (SHARED_TILE_SIZE / sizeof(struct Particle))

__global__ void layerUpdateKernel(float* layer, float* layer_copy, int layer_size, struct Particle* d_particles, int num_impacts, float threshold, float energy_scale) {
    __shared__ struct Particle s_particles[MAX_PARTICLES_PER_TILE];
    
    int myID = blockIdx.x * blockDim.x + threadIdx.x;   
    int tid = threadIdx.x;
    int num_tiles = (num_impacts + MAX_PARTICLES_PER_TILE - 1) / MAX_PARTICLES_PER_TILE;
    
    float total_energy_to_add = 0.0f;
    if (myID < layer_size) {
        total_energy_to_add = layer[myID];
    }

    for (int t = 0; t < num_tiles; t++) {

        // TILE BOUNDARIES CALCULATION
        int tile_start = t * MAX_PARTICLES_PER_TILE;
        int particles_in_tile = (num_impacts - tile_start > MAX_PARTICLES_PER_TILE) 
                                ? MAX_PARTICLES_PER_TILE 
                                : (num_impacts - tile_start);

        // COOPERATIVE LOADING
        for (int i = tid; i < particles_in_tile; i += blockDim.x) {
            s_particles[i] = d_particles[tile_start + i];
        }
        __syncthreads();

        // COMPUTATION
        if (myID < layer_size) {
            for (int j = 0; j < particles_in_tile; j++) {
                int position = s_particles[j].position;
                float energy = (float)s_particles[j].energy * energy_scale;

                int distance = abs(position - myID) + 1;
                float atenuacion = sqrtf((float)distance);
                float energy_k = energy / atenuacion;

                if (energy_k >= threshold || energy_k <= -threshold) {
                    total_energy_to_add += energy_k;
                }
            }
        }
        
        __syncthreads();
    }

    if (myID < layer_size) {
        layer_copy[myID] = total_energy_to_add;
    }
}

__global__ void layer_stencil_kernel(float* layer, float* layer_copy, int layer_size) {
    int globalID = blockIdx.x * blockDim.x + threadIdx.x; // Global thread ID
    int warpID = threadIdx.x % 32;  // Lane ID within the warp (0-31)

    if (globalID >= layer_size) return;

    // --- READ VALUES
    float val = layer_copy[globalID];
    float left  = __shfl_up_sync(0xffffffff, val, 1);
    float right = __shfl_down_sync(0xffffffff, val, 1);

    // --- HANDLE BOUNDARIES
    if (warpID == 0 && globalID > 0) { 
        // Read from global memory (lane -1 doesn't exist)
        left = layer_copy[globalID - 1]; 
    }
    
    if (warpID == 31 && globalID < layer_size - 1) { 
        // Read from global memory (lane 32 doesn't exist)
        right = layer_copy[globalID + 1];
    }

    // --- APPLY THE STENCIL
    if (globalID > 0 && globalID < layer_size - 1) {
        layer[globalID] = (left + val + right) / 3.0f;
    }
}

__global__ void local_max_kernel(float* layer, struct max_pos* max_per_block, int layer_size) {
    int myID = blockIdx.x * blockDim.x + threadIdx.x;
    int local_thread_id = threadIdx.x;
    int block_size = blockDim.x;

    __shared__ struct max_pos local_max[NUM_THREADS_PER_BLOCK];

    local_max[local_thread_id].max = -INFINITY; // Initialize to negative infinity
    local_max[local_thread_id].pos = -1;        // Initialize to invalid position

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

    // - PARTICLES ARRAY ALLOCATION ON DEVICE
    int max_storm_size = 0;
    for(int i=0; i<num_storms; i++) { 
        if(storms[i].size > max_storm_size) max_storm_size = storms[i].size; 
    }
    struct Particle *d_particles;
    cudaError_t err3 = cudaMalloc((void**)&d_particles, max_storm_size * sizeof(struct Particle));
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
        cudaMemcpy(d_particles, storms[i].posval, sizeof(struct Particle) * storms[i].size, cudaMemcpyHostToDevice);

        // - Update Layer (with dynamic shared memory)
        layerUpdateKernel<<<blocksPerGrid, threadsPerBlock>>>(d_layer, d_layer_copy, layer_size, d_particles, storms[i].size, threshold, energy_scale);
        
        // - Apply stancil (smoothing - 3 points average)
        layer_stencil_kernel<<<blocksPerGrid, threadsPerBlock>>>(d_layer, d_layer_copy, layer_size);

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
    cudaFree(d_particles);
    cudaFree(d_block_local_max);
    cudaFreeHost(layer);
}
```

## Modifiche 

- Usato shuffle in stencilKernel 
- layerUpdateKernel scrive direttamente in layer copy, cosi non dobbiamo fare la copia dopo

## Tempi

Questo non ha avuto un minusole miglioramento, ora stiamo costantemente sotto i 27ms