---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2026-02-20T15:16
updated: 2026-02-20T16:35
---
```c
#include <stdio.h>
#include <stdlib.h>
#include <math.h>
#include "energy_storms.h"

#include <cuda.h>

__device__ int getGlobalIdx_1D() {
    return blockIdx.x * blockDim.x + threadIdx.x;
}

__global__ void layerKernel(float* layer, int layer_size, int* d_posval, int num_impacts, float threshold) {
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

void core(int layer_size, int num_storms, Storm *storms, float *maximum, int *positions) {
    float threshold = THRESHOLD / layer_size;

    // - ALLOCATE HOST LAYER
    float *layer, *layer_copy;
    cudaError_t err1 = cudaMallocHost((void**)&layer,      layer_size * sizeof(float));
    cudaError_t err2 = cudaMallocHost((void**)&layer_copy, layer_size * sizeof(float));
    if (err1 != cudaSuccess || err2 != cudaSuccess) {
        printf("CUDA Host Memory allocation error\n");
        return;
    }
    memset(layer, 0, layer_size * sizeof(float));

    // - ALLOCATE DEVICE LAYER
    float *d_layer;
    cudaError_t err = cudaMalloc((void**)&d_layer, sizeof(float) * layer_size);
    if (err != cudaSuccess) {
        printf("CUDA Error allocating device layer: %s\n", cudaGetErrorString(err));
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

    // - DEFINE DIMENSIONS
    int threadsPerBlock = 256; 
    int blocksPerGrid = (layer_size + threadsPerBlock - 1) / threadsPerBlock; // Calculate blocks needed (ceil division)

    // ------------------------------------------------------------------------------------------
   
    for( int i=0; i<num_storms; i++) {

        // - Move the layer to device
        cudaMemcpy(d_layer, layer, sizeof(float) * layer_size, cudaMemcpyHostToDevice);
        
        // - Move the particles of the current storm to device
        int num_impacts = storms[i].size;
        cudaMemcpy(d_posval, storms[i].posval, sizeof(int) * num_impacts * 2, cudaMemcpyHostToDevice);

        // - Update Layer
        layerKernel<<<blocksPerGrid, threadsPerBlock>>>(d_layer, layer_size, d_posval, storms[i].size, threshold);

        // - Copy back the updated layer to host
        cudaDeviceSynchronize();
        cudaMemcpy(layer, d_layer, sizeof(float) * layer_size, cudaMemcpyDeviceToHost); // copy back to host
        
        // ----------------------------------------------------------------------------------

        /* 4.2. Energy relaxation between storms */
        /* 4.2.1. Copy values to the ancillary array */
        for( int k=0; k<layer_size; k++ )
            layer_copy[k] = layer[k];

        /* 4.2.2. Update layer using the ancillary values.
                  Skip updating the first and last positions */
        for( int k=1; k<layer_size-1; k++ )
            layer[k] = ( layer_copy[k-1] + layer_copy[k] + layer_copy[k+1] ) / 3;

        /* 4.3. Locate the maximum value in the layer, and its position */
        for( int k=1; k<layer_size-1; k++ ) {
            /* Check it only if it is a local maximum */
            if ( layer[k] > layer[k-1] && layer[k] > layer[k+1] ) {
                if ( layer[k] > maximum[i] ) {
                    maximum[i] = layer[k];
                    positions[i] = k;
                }
            }
        }
    }

    // Cleanup
    cudaFree(d_layer);
    cudaFreeHost(layer);
    cudaFreeHost(layer_copy);
}
```

Cosa abbiamo fatto dalla [[Cuda v1]]?
- Non ri inizzializziamo più il layer il layerKernel 20000, ma solo una per storm (da 400ms a 38ms)
  
### Why this is incredibly fast on a GPU:

You might look at that kernel and think, _"Wait, if every single thread is reading `d_posval[j*2]` at the same time, won't that cause a massive traffic jam in the GPU memory?"_

No! Because of how Warps execute in lockstep, all 32 threads in a warp will ask for `d_posval[0]` at the exact same nanosecond. The GPU hardware is smart enough to see this, read the value from global memory _once_, and broadcast it to all 32 threads simultaneously. It's a highly optimized memory access pattern.