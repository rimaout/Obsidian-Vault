---
type: Uni Note
class:
  - "[[Programmazione Sistemi Multicore (class)]]"
academic year: 2024/2025
related:
completed: false
created: 2025-11-04T19:00
updated: 2026-01-31T13:32
---
## Introduzione

Le operazioni collettive sono operazioni che coinvolgono tutti i processi di un gruppo di comunicazione (comunicatore), queste operazioni permettono di eseguire azioni coordinate tra tutti i processi, come la comunicazione di dati o la sincronizzazione.

Queste operazioni sono diventate particolarmente importanti nell’ultimo periodo in quanto sono utilizzate nella stragrande maggioranza dei programmi paralleli che vengono eseguiti per il training delle reti neurali odierne. Le grosse aziende di cup/gpu e di informatica, hanno iniziato a produrre delle proprie librerie proprietarie:
- NCCL (Nvidia)
- RCCL (AMD)
- OneCCL (Intel)
- MSCCL (Microsoft)

Infatti MPI durante le operazioni aggregate utilizza delle euristiche per stimare quale sia il miglior modo di condividere i dati fra i nodi, è possibile forzare tale decisione attraverso delle opportune variabili d’ambiente. Il punto è che MPI non è consapevole dell’hardware sul quale i processi sono eseguiti, per questo le aziende hanno iniziato a produrre librerie proprietarie, appositamente ottimizzate per girare sulle piattaforme dedicate.

>[!bug] Attenzione a questo errore
>
>Quando viene chiamata una funzione collettiva, è importante che **ogni processo** del comunicatore la chiami, altrimenti l’esecuzione rimane bloccata in uno stato di attesa, dato che ogni processo attende che tutti gli altri siano arrivati a tale operazione. 

## MPI_Reduce

`MPI_Reduce` permette di eseguire operazioni di aggregazione di risultati senza preoccuparci della logica di comunicazione per il trasferimento dei dati parziali. 

- Esempio esaustivo: [[Calcolo Integrale (MPI)]]

L'**output** è un `int`,  in input prende i seguenti parametri:
- `void* input_data_p` puntatore all'area di memoria in contenente i dati parziali da aggregare
- `void* output_data_p` puntatore all'area di memoria in cui verranno salvati il totale dei valori aggregati
- `int count` in numero di elementi da aggregare
- `MPI_Datatype datatype` il tipo dei valori
- `MPI_Op operator` è l’operazione di aggregazione
- `int dest_process` è il rank del processo che riceverà il risultato
- `MPI_Comm comm` è il comunicatore

>***Nota:*** `output_data_p` può essere impostato a `NULL` in tutti rank diversi da `dest_process`.

Le **operazioni di aggregazione** supportate da MPI sono le seguenti:

| Operazione | Significato                   |
| ---------- | ----------------------------- |
| MPI_MAX    | Massimo                       |
| MPI_MIN    | Minimo                        |
| MPI_SUM    | Somma                         |
| MPI_PROD   | Prodotto                      |
| MPI_LAND   | AND logico                    |
| MPI_BAND   | AND bit a bit                 |
| MPI_LOR    | OR logico                     |
| MPI_BOR    | OR bit a bit                  |
| MPI_LXOR   | XOR logico                    |
| MPI_BXOR   | XOR bit a bit                 |
| MPI_MAXLOC | Massimo insieme al suo indice |
| MPI_MINLOC | Minimo insieme al suo indice  |

È possibile anche definire delle operazioni personalizzate tramite la chiamata `MPI_Op_create`.

## MPI_Bcast

`PI_Bcast` che si occupa di eseguire il broadcast da un processo verso tutti gli altri. I parametri sono i seguenti :
- `void* data_p` puntatore all'area di memoria:
	- contenente i dati da condividere, se il processo è il `source_process`
	- che conterrà i dai ricevute, se il processo **non** è il `source_process`
- `int count` è il numero di elementi da condividere
- `MPI_Datatype datatype` è il tipo dei valori in questione
- `int source_process` è il rank del processo che condivide il valore
- `MPI_Comm comm` è il comunicatore

>[!note] Nota
>
>Utilizza una struttura ad albero che permette di suddividere il carico del lavoro su tutti i nodi e di non pesare solamente sul nodo mittente, creando un albero di condivisione.
>
>![[Pasted image 20251105162438.png|700]]

Un caso specifico in cui la `MPI_Bcast` è molto utile è quando si vuole leggere un input dell utente, infatti soltanto il processo radice (con rank 0) può interagire con l'`stdin`, e per questo una volta letto l'input molto spesso dovra poi essere condiviso con tutti gli altri nodi, esempio: [[User Input in MPI]].

## MPI_Allreduce

Se si vuole fare un operazione di aggregato, per poi avere il risultato condiviso fra tutti i processi, concettualmente, ciò equivale ad eseguire una `MPI_Reduce` seguita da una `MPI_Bcast`.

MPI fornisce una funzione, ottimizzata per fare proprio questo ossia `MPI_Allreduce` , con i seguenti parametri:
- `void* input_data_p` puntatore all'area di memoria in contenente i dati parziali da aggregare
- `void* output_data_p` puntatore all'area di memoria in cui verranno salvati il totale dei valori aggregati (e condivisi)
- `int count` in numero di elementi da aggregare (e condividere)
- `MPI_Datatype datatype` il tipo dei valori
- `MPI_Op operator` è l’operazione di aggregazione
- `MPI_Comm comm` è il comunicatore

I parametri sono identici alla `MPI_Reduce`, eccetto per l’assenza del processo di destinazione, dato che in questo caso, ogni processo avrà il risultato.