---
Main Moc: "[[Uni MOC]]"
academic year: 2025/2026
created: 2025-09-23T17:21
updated: 2025-09-23T18:39
---
**Chapters:**
- Why parallel programming
- Parallel hardware and parallel softare
- Distributed programming with MPI
- Shared-memory programming with Pthreads
- Shared memory programming with openMP
- GPU programming with CUDA

## Why parallel programming

sdmnsad,nf++

Il costo del sommare i valori dei tread cambia se:
- utilizziamo un master allora nodo master in questo caso costa `p-1` (dove `p` è il numero di thread)
- utilizzando una struttura ad albero binario il nodo con il soto più alto è log_2(p)