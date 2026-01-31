---
type: Uni Note
class:
  - "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2024-09-28T16:52
updated: 2026-01-31T13:32
---

>[!abstract] Related
>- [Sistemi Operativi 1 (class)](app://obsidian.md/Sistemi%20Operativi%201%20\(class\))

---
## Introduzione

>[!note] Definizione
>La cache è una memoria relativamente piccola e veloce, che generalmente si trova tra la memoria principale (RAM) e la CPU (Unità Centrale di Elaborazione) e funziona come un buffer che memorizza i dati e le istruzioni più recentemente utilizzati.
>
>![[Pasted image 20240928170112.png|600]]

>[!warning] Info di Base
>- Le cache, anche piccole, hanno un *grade impatto nel migliorare le performance* di sistema.
>- La CPU prima di accedere alla RAM controlla se i dati di cui ha bisogno sono già presenti all’interno della cache.
>- Serve mantenere **consistenza** tra *Cache* e *RAM*, questo vuol dire che ogni volta che un contenuto nella cache è modificato allora deve essere modificata anche la su "versione" in RAM.
>- La cache è *invisibile* sia al programmate (anche in assembler) che al sistema operativo, infatti è completamente gestita dall'hardware.
>  
>>***Nota:*** Anche se il sistema operativo non può vedere la cache, può comunque **disabilitare il caching** e inoltre può decidere [[#^299438|la politica di scrittura]], ad esempio Linux non la spegne mai e utilizza sempre write-back.

## Struttura

Data una memoria RAM parla con $2^{n}$ indirizzi di memoria disponibili, suddivisi in blocchi di dimensione $K$ (il numero di parole in un blocco).

Una memoria cache avrà in numero di blocchi (`C`) molto minore al numero di blocchi della RAM ($\frac{2^{n}}{K}$). Questo significa che non tutti i blocchi della RAM possono essere memorizzati nella cache contemporaneamente.

Per questo motivo viene utilizzato il **Tag**, un identificatore che indica quale blocco di memoria RAM è attualmente memorizzato nella cache. Quindi il numero di bit nel Tag deve essere sufficiente per rappresentare tutti i blocchi della memoria RAM.

Per questo otteniamo che:

$$
Tag \geq \log_{2} ​\left( \frac{2^{n}}{k}​ \right)
$$

![[Pasted image 20250821171629.png|800]]

>[!note] Misura dei Blocchi
>
>Avere dei blocchi di dimensione più grande, potrebbe sembrare una cosa positiva infatti, teoricamente aumenta la probabilità di successo di accesso (HIT), dato che: 
>- Quando si aumenta la dimensione del blocco, si tende a memorizzare più dati in un singolo accesso. 
>- Questo significa che se un programma richiede un dato, è probabile che richieda anche dati adiacenti (**località dei riferimenti**).
>- Quindi, se il blocco è più grande, è più probabile che i dati richiesti siano già presenti nella cache.
>
>Però in pratica avere dei blocchi troppo grandi può essere uno svantaggio, infatti:
>- ***Occupazione di Spazio***: Blocchi più grandi occupano più spazio per ogni linea, riducendo il numero di linee memorizzabili nella cache.
>- ***Aumento delle Rimozioni di Blocchi Utili***: Meno linee disponibili portano a rimozioni più frequenti, aumentando il rischio di sovrascrivere blocchi utili.
>- ***Aumento dei Miss Complessivi***: Con meno linee e più rimozioni, diminuisce la probabilità che i dati siano già in cache, aumentando i miss.

## Funzionamento

>[!note] Procedimento Lettura
>![[Pasted image 20240927144423.png|500]]

>[!note] Algoritmi di Rimpiazzamento
>
>Determina in che modo scegliere quale blocco va rimpiazzato, tipicamente si usa l’algoritmo **LRU (Least Recently Used)** che rimpiazza il blocco usato meno recentemente ovvero il più vecchio presente in Cache.

>[!note] Politiche di scrittura
>
>Una politica che stabilisce quando e come le modifiche nella cache vengono propagate alla memoria principale; definisce se aggiornare la memoria immediatamente o ritardare l'aggiornamento e come tenere traccia dei blocchi modificati.
>
>***Write-through:*** - ogni modifica a un blocco in cache viene immediatamente scritta anche in memoria principale.
>
> - Pro: memoria sempre aggiornata. 
> - Contro: molte scritture, aumentano il traffico nel bus.
>
>***Write-back*** - le modifiche restano in cache e vengono scritte in memoria principale solo quando il blocco viene rimpiazzato (serve un bit "dirty" per ogni blocco modificato).
>
>- Pro: minimizzare le operazioni di scrittura per ridurre latenza e traffico sul bus.
>- Contro: la memoria principale può essere incoerente rispetto alla cache fino a quando i blocchi modificati non vengono scritti indietro.

^299438

## Cache Gerarchica

Solitamente non esiste soltanto una cache all'interno della cpu ma ci sono i più cache alcune più piccole e veloci e altre più grandi ma più lente.

>[!note] Sistemi multi core
>Nei sistemi multicore, solitamente, è presente una o più cache per ogni core, e poi una cache generale.
>
>![[Pasted image 20240927150510.png|350]]

