---
type: Uni Note
class:
  - "[[Programmazione Sistemi Multicore (class)]]"
academic year: 2024/2025
related:
completed: false
created: 2025-11-04T19:00
updated: 2025-11-04T19:05
---
## Introduzione

Se riprendiamo l'esempio del [[Calcolo Integrale (MPI)|calcolo dell'integrale utilizzando MPI]] è possibile notare che il processo di rank zero ha un carico di lavoro superiore rispetto ogni altro processo, infatti, quest’ultimo oltre la somma dei suoi trapezi locali, deve calcolare la somma totale, inoltre deve occuparsi di ricevere i dati da tutti gli altri processi.

