---
Main Moc: "[[Uni MOC]]"
academic year: 2025/2026
created: 2025-09-23T17:21
updated: 2025-10-01T15:36
---
[sito corso]()
[[C MOC]]

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

## C


Memoria divisa in stack e heap:
- *stack*: parte statica, utilizzata per l'esecuzione delle funzioni
- *heap*: parte dinamica, ovvero dope la dimensione degli elementi può variare (esempio array dinamici)


Per allocare nella memoria dinamica utilizziamo `malloc`.

```c
void* malloc(int size)
```

Funzione che prendi in input in numero di byte e riserva un buffer di quella dimensione ritornando un puntatore al primo indirizzo del buffer.
- è un puntatore a void (senza tipo) quindi dobbiamo castrato nel tipo che vogliamo utilizzare.
- se l'operazione ha un qualsiasi problema nell allocazione, ritorna un puntatore a null, quindi prima di qualsiasi operazione dovremmo controllare che il puntatore non sia null

Permette di ridurre o elementare la grandezza di un buffer, quindi prende in input un puntatore ad un buffer e la nuova grandezza e ritorna un puntatore alla nuovo area di memoria.

```c
void* realloc(void* ptr, int size)
```

Se non c'è abbastanza spazio in quella sezione di memoria per estendere, allora automaticamente verrà cercata un altra memoria abbastanza grande da poter effettuare la riallocazione in cui verranno spostati tutti i dati.

**calloc** riserva un buffer di (size x numElements) bytes, gli assegniamo un valore di default e ne ritorna l'indirizzo.

```c
void* calloc(int numElements, int size)
```

