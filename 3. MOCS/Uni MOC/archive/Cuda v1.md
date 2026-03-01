---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2026-02-20T13:03
updated: 2026-02-20T15:18
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

// IDEA:
// - creiamo in thread per ogni elemento del layer

__device__ void update(float *layer, int layer_size, int k, int pos, float energy, float threshold) {
    int distance = abs(pos - k) + 1;
    float atenuacion = sqrtf((float)distance);
    float energy_k = energy / atenuacion;

    if (energy_k >= threshold || energy_k <= -threshold)
        layer[k] += energy_k;
}

__global__ void layerKernel(float* layer, int layer_size, int impact_position, float energy, float threshold) {
    int myID = getGlobalIdx_1D();

    // BOUNDARY CHECK: crucial because (Grid * Block) might be larger than layer_size
    if (myID < layer_size) {
        update(layer, layer_size, myID, impact_position, energy, threshold);
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
        printf("CUDA Error: %s\n", cudaGetErrorString(err));
        return;
    }

    // - DEFINE DIMENSIONS
    int threadsPerBlock = 256; 
    int blocksPerGrid = (layer_size + threadsPerBlock - 1) / threadsPerBlock; // Calculate blocks needed (ceil division)

    // ------------------------------------------------------------------------------------------
   
    for( int i=0; i<num_storms; i++) {

        // - Move the layer to device
        cudaMemcpy(d_layer, layer, sizeof(float) * layer_size, cudaMemcpyHostToDevice);

        // - Update Layer
        for( int j=0; j<storms[i].size; j++ ) {
            float energy = (float)storms[i].posval[j*2+1] * 1000 / layer_size;
            int position = storms[i].posval[j*2];

            layerKernel<<<blocksPerGrid, threadsPerBlock>>>(d_layer, layer_size, position, energy, threshold);   
        }

        // - Copy back the updated layer to host
        cudaDeviceSynchronize();
        cudaMemcpy(layer, d_layer, sizeof(float) * layer_size, cudaMemcpyDeviceToHost); // copy back to host
        
        // ------------------------------------------------------------------------------------------

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

Problemi:
- Non facciamo tutto in GPU, quindi la cpu e la gpu ad ogni storm devono essere sincronizzate e fare memcopy (molto costoso) -> obbiettivo parallelizzare tutto
- avendo messo layer kernel dentro il for `for( int j=0; j<storms[i].size; j++ )` viene ri inizializzato 20000 volte (almeno nel test che abbiamo fato), soluzione fare tutto in un solo kernel, ovvero ad ogni thread (che rappresenta una cella del layer) facciamo fare l'update su tutte le particelle della storm. Risolto in [[Cuda v2]]

