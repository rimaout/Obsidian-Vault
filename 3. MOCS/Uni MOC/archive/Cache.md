---
type: Uni Note
class:
  - "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related: 
completed: false
created: 2024-09-28T16:52
updated: 2024-10-01T13:57
---
>[!abstract] Index
>1. 

>[!abstract] Related
>- 

---
## Introduzione

>[!note] Definizione
>La Cache è una memoria relativamente picco la e veloce, che viene utilizzata per memorizzare temporaneamente i dati e le istruzioni più frequentemente utilizzati.
>
>La memoria cache si trova generalmente tra la memoria principale (RAM) e la CPU (Unità Centrale di Elaborazione) e funziona come un buffer che memorizza i dati e le istruzioni più recentemente utilizzati.
>
>![[Pasted image 20240928170112.png|500]]

>[!warning] Info di Base
>- Cache anche se piccole hanno un grade impatto nel migliorare le performance di sistema
> - Il processore prima di accedere alla ram controlla se i dati che gli servono sono già all’interno della cache.
>- Serve mantenere consistenza tra **Cache** e **RAM**, questo vuol dire che ogni volta che un contenuto nella cache è modificato allora deve essere modificata anche la su "versione" in RAM.
>- La Cache è invisibile hai programmi compreso il sistema operativo, infatti è completamente gestita dall'hardware.

---
## Funzionamento

>[!note] Procedimelo Lettura
>![[Pasted image 20240927144423.png|500]]

>[!note] Misura dei Blocchi
>- incrementare la misura del blocco aumenta il numero di accessi riusciti (HIT)
>- ma incrementarla troppo è controproducente: 
>	- All'aumentare della grandezza dei blocchi si riduce il linee di cache
>	- Questo che vuol dire saranno di più i dati che vengono rimossi 
>	- il che abbassa la probabilità di accesso riusci

>[!note] Algoritmi di Ripianamento
>Algoritmo Least-Recently-Used (LRU): si rimpiazza il blocco usato meno di recente (quindi, pi`u vecchio)

>[!note] Politiche di Scritture
>- determina quando occorre scrivere in memoria può accadere ogni volta che un blocco viene modificato (write-through)
>- può accadere quando il blocco è rimpiazzato (write-back) 
>- occorre minimizzare le operazioni di scrittura 
>- questo vuol dire che la memoria può trovarsi in uno stato “obsoleto”, ovvero non in linea con il contenuto della cache

---
## Cache Gerarchica

Solitamente non esiste soltanto una cache all'interno della cpu ma ci sono i più cache alcune più piccole e veloci e altre più grandi ma più lente.

>[!note] Sistemi multi core
>Nei sistemi multicore, solitamente, è presente una o più cache per ogni core, e poi una cache generale.
>
>![[Pasted image 20240927150510.png|350]]
