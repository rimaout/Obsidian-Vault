---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2025-10-07T17:18
updated: 2025-10-11T16:25
---
Scriveremo programmi che sono esplicitamente paralleli, per farlo useremo 4 differenti estensioni di `C`:
- Message-Passing Interface (MPI) (Library)
- Posix Threads (Pthreads) (Library)
- OpenMP (Library + Compiler)
- CUDA (Library + Compiler)
  
Esistono libreria ad alto livello ma sacrificano le performance per la facilità d'uso.

## Tipologie di programmazione parallela

>[!note] Memoria
>**Shared-memory** - i core possono condividere l'accesso alla memoria del computer. Questo permette di far coordinare i core scambiando si "messaggi"  attraverso le aree di memoria condivise.
>
>**Distributed-memory** - ogni core ha la sua memoria privata, per comunicare sono obbligati ad utilizzare una rete.

>[!note] Control Unit
>
>**Multiple-Instruction Multiple-Data (MIMD)** - ogni core ha la sua control unit e può lavorare indipendentemente dagli altri core.
>
>**Single-Instruction Multiple-Data (SIMD)** - i core condividono la control unit, quindi devono tutti eseguire la stessa operazione, se non avviene allora una parte i core starà in idle (es. le gpu).
>- ***Nota:*** come vedremo non è vero che tutti i core devo fare le stesse operazioni, infatti molto spesso i core sono divisi in cluster che condividono la stessa contro unit, e core nello stesso cluster devono effettuare le stesse operazioni 
>- Per questo motivo cercheremo di scrivere codice che ha meno `if` e brach possibili, in modo tale da ridurre le possibili operazioni che possono differire tra due core.  

Le librerie che abbiamo visto si comportano in questo modo:

![[Pasted image 20251007173300.png|600]]

## Concurrent vs. Parallel vs. Distributed


##  Hardware

Scriveremo in C proprio perche ci permette di avere controllo diretto sul'hardware in modo tale da ridurre le perdire dovute all'astrazione . Però questo signnifica che dobbiamo capire come funziona l'hardware su cui lavoreremo.

### jlflkaj

L'obbiettivo quando si scrive codice è di sfruttare al massimo la località dei dati in modo tale da aumentare la probabilità da effetuaare più accessi in cache possibili (e meno in disco)

----



## Single-Program Multiple-Data (SPMD)

..òòkj


```c
#include <stdio.h>
#include <mpi.h>

int main(void) {
	MPI_Init(NULL, NULL);
	printf(“hello, world\n”);
	MPI_Finalize();
	return 0;
}
```

Tutti i programmi MPI hanno sempre due chiamata:
- **Chiamata di inizializzazione:** `MPI_Init` che inizializza la libreria MPI
- **Chiamata di finalizzazione:** `MPI_Finalize()` che specifica la fine del codice MPI

Tutte le chiamate MPI dovranno essere scritte all’interno del codice tra la chiamata di inizializzazione e di finalizzazione.

>[!note] MPI_Init
>
>Dice a MPI di fare il setup iniziale, questa è la firma della funzione:
>
>```c
>int MPI_Init(int* argc_p, char*** argv_p)
>``` 
>
>Dove:
>- `argc_p` è il puntatore al campo `agrc` del main
>- `argv_p` è il puntatore al campo `agrv` del main

>[!note] MPI_Finalize
>
>Dice a MPI di pulire qualsiasi cosa allocata dal programma.
>
>```c
>int MPI_Finalize(void)
>```


