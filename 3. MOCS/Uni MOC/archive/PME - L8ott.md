---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2025-10-08T14:31
updated: 2025-10-11T15:07
---
## Sending order

MPI requires that messages be non-overtaking. This means that if process `q` sends two messages to process `r`, then the first message sent by `q` must be available to `r` before the second message.

However, there is no restriction on the arrival of messages sent from different processes

## Data Types

| MPI Datatype       | C Datatype           |
| ------------------ | -------------------- |
| MPI_CHAR           | signed char          |
| MPI_SHORT          | signed short int     |
| MPI_INT            | signed int           |
| MPI_LONG           | signed long int      |
| MPI_LONG_LONG      | signed long long int |
| MPI_UNSIGNED_CHAR  | unsigned char        |
| MPI_UNSIGNED_SHORT | unsigned short int   |
| MPI_UNSIGNED       | unsigned int         |
| MPI_UNSIGNED_LONG  | unsigned long int    |
| MPI_FLOAT          | float                |
| MPI_DOUBLE         | double               |
| MPI_LONG_DOUBLE    | long double          |
| MPI_BYTE           |                      |
| MPI PACKED         |                      |

## Come funziona l'invio i messaggi

Un messaggio è di secusse se:
- `recvtype = send_type`
- `recv_buf_sz >= send_buf_sz`

Ma un ricevitore può ricevere un messaggio senza sapere:
- the amount of data in the message,
- the sender of the message (`MPI_ANY_SOURCE`)
- or the tag of the message (`MPI_ANY_TAG`),

>[!note] Status pointer
>![[Pasted image 20251008144301.png|500]]
>
>Non lo utilizzeremo molto

>[!note] Come sapere quanti dati stiamo ricevendo 
>
>Poissiamo usare l'operazione:
>
>![[Pasted image 20251008144427.png|500]]


## Garanzie

Come funziona la send, Quando effettuiamo una send, non abbiamo nessuna garanzia su quello che sta avvenendo, non sappiamo se è stato inviato se è arrivato.

L'unica garanzia che abbiamo è che i dati trasmessi sono quelli che abbiamo passato alla operazione send, attraverso il buffer, quando abbiamo chiamato l’operazione.
- Questo significa se modifichiamo i dati dopo aver chiamato la send, possiamo essere sicuri che verranno inviati quelli originali e non i modificati.
## Problemi con Send and Receive

MPI è uno standard ma non è detto che tutte le implementazioni di MPI abbiano gli stessi identici risultati, le uniche assunzione che possiamo fare sono [[#Garanzie]].

MPI_Send may behave differently with regard to buffer size, cutoffs and blocking

MPI_Recv always blocks until a matching message is received.

Even if you know your MPI implementation, stick to what defined by the standard (i.e., don’t assume that the send returns immediately for small buffers)! Otherwise your code will not be portable.
  


![[Pasted image 20251008145732.png|700]]

## Cosa succede quando effettuo una send

![[Pasted image 20251008145801.png|800]]

- Come possiamo vedere avvengono diverse copie dei dati durante tutto il procedimento di invio
- Ci sono alcuni costi che sono fissi, ovvero che non dipendono dalla dimensione del dati inviati, quindi conviene cercare di raggruppare i dati per ridurre il numero di send e ridurre le perdite dofute hai costi fissi.

## Point-to-Point Communication Mode


## Non-Blocking Communication

Nelle chiamate non bloccanti (anche dette comunicazioni immediate) 

`Isend` (è una send immediata)

>[!danger] Downside
>
>