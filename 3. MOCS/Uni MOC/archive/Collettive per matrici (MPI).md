---
type: Uni Note
class:
  - "[[Programmazione Sistemi Multicore (class)]]"
academic year: 2024/2025
related:
completed: false
created: 2025-11-10T14:34
updated: 2025-11-10T17:01
---
## Scatter

`MPI_Scatter` è un operazione collettiva che permette di inviare a ciascun processo un segmento distinto di un array più grande che esiste solo nel processo radice.

L'effetto è come se il processo radice eseguisse tante operazioni di invio (`MPI_Send`), una per ogni processo nel gruppo, e ciascun processo eseguisse una ricezione  `MPI_Recv`) corrispondente.

![[Pasted image 20251110144436.png|450]]

 I parametri della funzione sono i seguenti:
- `void *send_buf_p` il buffer contenente il vettore da inviare
- `int send_count` il numero di elementi da inviare ad ogni processo (*non il numero di elementi totali del vettore*)
- `MPI_Datatype send_type` il tipo degli elementi del vettore
- `void *recv_buf_p` il buffer che conterrà la frazione di vettore ricevuta (*per il mittente, può coincidere con il buffer di invio*)
- `int recv_count` analogo a send_count
- `MPI_Datatype recv_type` analogo a send_type
- `int src_proc `il rank del processo che condividerà il vettore
- `MPI_Comm comm` il comunicatore in questione

>[!note] Cosa Succede 
>
>```c
>MPI_Scatter(buff, 3, MPI_INT, dest, 3 MPI_INT, 0, MPI_COMM_WORLD);
>```
>
>![[Pasted image 20251110145327.png|800]]
>
>Il rank che effettua l'invio (in questo caso il rank 0) può anche modificare direttamente l'array che viene inviato utilizzando `MPI_IN_PLACE`.
>
>```c
>if(rank == 0) {
>	MPI_Scatter(buff, 3, MPI_INT, MPI_IN_PLACE, 3, MPI_INT, 0, MPI_COMM_WORLD);
>} else {
>	MPI_Scatter(buff, 3, MPI_INT, dest, 3, MPI_INT, 0, MPI_COMM_WORLD);
>}
>```
>
>![[Pasted image 20251110152818.png|800]]