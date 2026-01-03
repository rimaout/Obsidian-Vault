---
type: Uni Note
class:
  - "[[Programmazione Sistemi Multicore (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-11-04T18:06
updated: 2025-11-04T18:43
---
## Esempio Loop con chiamate non bloccanti

Il seguente esempio mostra un programma in cui n processi (in questo caso 4) si scambiano informazioni in una configurazione "ad anello", in cui ognuno invia e riceve a/da i suoi vicini, l’utilizzo di chiamate non bloccanti è utile per evitare situazioni di deadlock.

```c
#include "mpi.h"
#include "stdio.h"

int main(int argc, char *argv[]) {

    int num_task, rank, next, prev, buf[2], value_to_send;
    MPI_Request reqs[4];
    MPI_Status stats[4];

    MPI_Init(NULL, NULL);
    MPI_Comm_size(MPI_COMM_WORLD, &num_task);
    MPI_Comm_rank(MPI_COMM_WORLD, &rank);

    // Calculation of neighbors in the ring
    prev = (rank - 1 + num_task) % num_task;
    next = (rank + 1) % num_task;

    // Each process sends rank * 10
    value_to_send = rank * 10;

    // Non-blocking communication with neighbors
    MPI_Irecv(&buf[0], 1, MPI_INT, prev, 0, MPI_COMM_WORLD, &reqs[0]);
    MPI_Irecv(&buf[1], 1, MPI_INT, next, 0, MPI_COMM_WORLD, &reqs[1]);
    MPI_Isend(&value_to_send, 1, MPI_INT, prev, 0, MPI_COMM_WORLD, &reqs[2]);
    MPI_Isend(&value_to_send, 1, MPI_INT, next, 0, MPI_COMM_WORLD, &reqs[3]);

	// --- Do computation here to overlap with communication --- 
	int result = 0; 
	for (int i = 0; i < 1000000; ++i) {
		result += rank * i; // Example: simulate computational work 
	} 
	// ---------------------------------------------------------

	// Wait for all non-blocking communications to finish
    MPI_Waitall(4, reqs, stats); 

    // Print received values
    printf("Process %d received %d from prev (rank %d), %d from next (rank %d)\n",
           rank, buf[0], prev, buf[1], next);
	
    MPI_Finalize();
    return 0;
}
```

>[!warning] Output
>
>Dopo aver eseguito il codice con `mpirun -np 4 ./a.out`, otteniamo in output: 
>
>```txt
>Process 2 received 10 from prev (rank 1), 30 from next (rank 3)
>Process 0 received 30 from prev (rank 3), 10 from next (rank 1)
>Process 3 received 20 from prev (rank 2), 0 from next (rank 0)
>Process 1 received 0 from prev (rank 0), 20 from next (rank 2)
>```

>[!note] Nota
>
>In questo esempio mostriamo anche che, grazie all'utilizzo delle chiamate non bloccanti `MPI_Irecv` e `MPI_Isend`, è possibile effettuare operazioni di calcolo tra l'avvio della comunicazione e la sincronizzazione finale (`MPI_Waitall`). In questo modo si può sovrapporre comunicazione e calcolo, ottimizzando l'efficienza del programma parallelo.

