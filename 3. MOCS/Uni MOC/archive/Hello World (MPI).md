---
type: Uni Note
class:
  - "[[Programmazione Sistemi Multicore (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-11-03T12:22
updated: 2025-11-04T18:06
---
## Richiesta

Implementare un programma MPI che soddisfi i seguenti requisiti:
1. Ogni processo deve creare un messaggio di saluto contenente il proprio identificativo (rank) e il numero totale di processi
2. I processi non-radice devono inviare il proprio messaggio al processo radice (rank 0)
3. Il processo radice deve:
    - Stampare il proprio messaggio
    - Ricevere e stampare i messaggi da tutti gli altri processi in ordine crescente di rank
4. Il programma deve correttamente inizializzare (`MPI_Init`) e finalizzare (`MPI_Finalize`) l'ambiente MPI

**Formato richiesto del messaggio:** "Hello, World! I am process %d of %d."
- dove il primo `%d` rappresenta il rank del processo e il secondo il numero totale di processi nel comunicatore.

## Soluzione Send/Recv

```c
#include <stdio.h>
#include <string.h>
#include <mpi.h>

int main(void) {
    int my_rank, comm_size;

    // Initialize MPI environment
    MPI_Init(NULL, NULL);
    MPI_Comm_rank(MPI_COMM_WORLD, &my_rank);
    MPI_Comm_size(MPI_COMM_WORLD, &comm_size);

    // Create greeting message
    char message[64];
    sprintf(message, "Hello, World! I am process %d of %d.\n", my_rank, comm_size);

    if (my_rank != 0) {
        // Non-root processes send their message to root
        MPI_Send(message, strlen(message) + 1, MPI_CHAR, 0, 0, MPI_COMM_WORLD);
    } else {
        // Root process prints its own message first
        printf("%s", message);
        
        // Then receives and prints messages from other processes in order
        for (int i = 1; i < comm_size; i++) {
            MPI_Recv(message, 64, MPI_CHAR, i, 0, MPI_COMM_WORLD, MPI_STATUS_IGNORE);
            printf("%s", message);
        }
    }

    // Finalize MPI environment
    MPI_Finalize();
    return 0;
}
```

>_**Nota:**_ Qui ho usato `strlen()` ma non so se rende il programma più veloce o più lento.
> - Infatti rende più efficiente la trasmissione delle informazioni
> - Ma `strlen()` ha un costo proporzionale alla lunghezza della stringa in input (dato che cerca il carattere `\0`)
>
> Probabilmente in questo contesto in cui la stringa più corta possibile è di 45 byte e quella più lunga è di 64, quindi **con un risparmio massimo di 19 byte**, conviene usare direttamente 64 byte fisso per evitare l'overhead computazionale di `strlen()`

## Soluzione Scatter/Gather

```c
#include <stdio.h>
#include <mpi.h>

int main(void) {
    int my_rank, comm_size;

    // Initialize MPI environment
    MPI_Init(NULL, NULL);
    MPI_Comm_rank(MPI_COMM_WORLD, &my_rank);
    MPI_Comm_size(MPI_COMM_WORLD, &comm_size);

    // Create greeting message
    char send_buffer[64];
    sprintf(send_buffer, "Hello, World! I am process %d of %d.\n", my_rank, comm_size);

    if (my_rank == 0) {
        // Root process receives all messages
        char recv_buffer[comm_size][64];
        MPI_Gather(send_buffer, 64, MPI_CHAR, recv_buffer, 64, MPI_CHAR, 0, MPI_COMM_WORLD);
        
        // Print all messages in order
        for (int i = 0; i < comm_size; i++) {
            printf("%s", recv_buffer[i]);
        }
    } else {
        // Non-root processes send their message
        MPI_Gather(send_buffer, 64, MPI_CHAR, NULL, 0, MPI_CHAR, 0, MPI_COMM_WORLD);
    }

    // Finalize MPI environment
    MPI_Finalize();
    return 0;
}
```

>***Nota:*** Teoricamente utilizzare `MPI_Gather` è più efficiente rispetto a usare `send/recv` manuale perché le operazioni collettive utilizzano algoritmi ottimizzati (come alberi binari) che riducono la latenza. Inoltre, essendo una chiamata collettiva sincronizzata tra tutti i processi, l'implementazione MPI può coordinare e sovrapporre le comunicazioni in parallelo, invece di gestirle sequenzialmente come avviene in un ciclo di `recv`.

