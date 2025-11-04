---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2025-10-29T14:20
updated: 2025-10-29T15:14
---
MPI è utilizzato per eseguire il parallelismo su più nodi, poi CUDA è utilizzato per parallelizaare il codice eseguito sui core della GPU, Pthread/OpenMP è utilizato per prallelizare il codice in esecuzione sui core della CPU.

**In questo corso non vederemo Pthread dato che è già stato visto a [[Sistemi Operativi 2 (class)]] e perché è meno intuitivo di OpenMP**

djsflksjdflkòjfadsglkòjdfslakò

## Thereading Levels in MPI

**MPI_THREAD_SINGLE**: il rank non ha il permesso di utilizzare più thread, quindi è equivalente a chiamare `MPI_Init`. QUindi non si può utilizzare ne Ptheread ne OpenMP

**MPI_THREAD_FUNNELED** 

**MPI_THREAD_SERIALIZED**

**MPI_THREAD_MULTIPLE** 