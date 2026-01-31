---
type: Uni Note
class:
  - "[[Programmazione Sistemi Multicore (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-11-05T16:40
updated: 2026-01-31T13:32
---
In MPI la lettura dell'input dell'utente può essere fatta fatta soltanto dal processo con rank 0, infatti è l'unico che può interagire con l'`stdin`, quindi una volta effettuata la lettura il valore dovrà poi essere comunicato ai restanti processi.

Per effettuare questa comunicazione potremmo utilizzare:
- delle `MPI_Send` dal rank 0 dirette a tutti gli altri processi
- delle `MPI_Recv` su tutti i rank diversi da 0

Questa versione però pesa eccessivamente sul rank 0 dato che sarà lui a dover fare tutte le send verso gli altri nodi.

Una soluzione migliore consiste nel suddividere il carico facendo si che il processo 0 condivida i dati con due altri processi, e questi due li condividano a loro volta con altri due processi ciascuno, creando un albero di condivisione.

Però grazie ad `MPI_Bcast` non dobbiamo implementare questa struttura da soli, in quanto in automatico sceglierà l’algoritmo più ottimizzato per effettuare la broadcast.

```c
void Get_input(int my_rank, int a, int b, int n) {
	if (my_rank == 0) {
		printf("Enter 3 integers:\n");
		scanf("%d %d %d", &a, &b, &n);
	}
	MPI_Bcast(a, 1, MPI_INT, 0 MPI_COMM_WORLD);
	MPI_Bcast(b, 1, MPI_INT, 0 MPI_COMM_WORLD);
	MPI_Bcast(c, 1, MPI_INT, 0 MPI_COMM_WORLD);
}
```
