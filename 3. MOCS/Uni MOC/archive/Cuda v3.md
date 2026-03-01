---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2026-02-20T16:36
updated: 2026-02-26T10:36
---
```c
#include <stdio.h>
#include <stdlib.h>
#include <math.h>
#include "energy_storms.h"

#include <cuda.h>

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

void core(int layer_size, int num_storms, Storm *storms, float *maximum, int *positions) {
    float threshold = THRESHOLD / layer_size;

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
    cudaError_t err1 = cudaMalloc((void**)&d_layer, sizeof(float) * layer_size);
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

    // - DEFINE DIMENSIONS
    int threadsPerBlock = 256; 
    int blocksPerGrid = (layer_size + threadsPerBlock - 1) / threadsPerBlock; // Calculate blocks needed (ceil division)

    // ------------------------------------------------------------------------------------------
   
    for( int i=0; i<num_storms; i++) {

        // - Move the layer to device
        cudaMemcpy(d_layer, layer, sizeof(float) * layer_size, cudaMemcpyHostToDevice);
        
        // - Move the particles of the current storm to device
        cudaMemcpy(d_posval, storms[i].posval, sizeof(int) * storms[i].size * 2, cudaMemcpyHostToDevice);

        // - Update Layer
        layerUpdateKernel<<<blocksPerGrid, threadsPerBlock>>>(d_layer, layer_size, d_posval, storms[i].size, threshold);

        // Copy layer to layer_copy for the next step
        cudaMemcpy(d_layer_copy, d_layer, sizeof(float) * layer_size, cudaMemcpyDeviceToDevice);
        
        // - Apply stancil (smoothing - 3 points average)
        layer_stancil_kernel<<<blocksPerGrid, threadsPerBlock>>>(d_layer, d_layer_copy, layer_size);

        // - Copy back the updated layer to host
        cudaDeviceSynchronize();
        cudaMemcpy(layer, d_layer, sizeof(float) * layer_size, cudaMemcpyDeviceToHost); // copy back to host
        
        // -------------------------------------------------------------------------------

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
    cudaFree(d_layer_copy);
    cudaFree(d_posval);
    cudaFreeHost(layer);
}
```


Qui abbiamo fatto una versione base dello stancil

TODO: 
- in futuro dobbiamo usare una array temporaneo salvato nella memoria shared per evitare di scrivere e leggere in ram in continuazione.
- Finire di parallelizzare la ricerca del massimo, infatti ora la gpu deve mandare alla cpu tutto il layer dopo ogni storm (costoso), soluzione aprallelizare anche il massimo in moda tale da tenere sembpre in gpu totto il layer e mandare soltanto una piccola lista di massimi locali. (fatto in [[Cuda v4|v4]])




