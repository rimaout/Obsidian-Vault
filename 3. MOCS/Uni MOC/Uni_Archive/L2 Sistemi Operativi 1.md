---
type: Uni Note
class: 
academic year: 2023/2024
related: 
completed: false
created: 2024-09-27T13:16
updated: 2024-09-27T17:49
---
>[!abstract] Index
>1. 

>[!abstract] Related
>- 

---


Uno stack è una sezione di memoria che viene assegnato ad un processo.

![[Pasted image 20240927132738.png|500]]


## Interruzioni

>[!note] Sequenziali
>![[Pasted image 20240927132910.png|400]]

>[!note] Annidate
>![[Pasted image 20240927132938.png|400]]

## Operazioni di I/O

>[!note] Input Output **Programmato**
>- Vecchio modo di fare.
>- L’azione di lettura o scrittura viene effettuata da un modulo dedicato (non il processore).
>- Non ci sono interruzioni, quindi il processore deve attendere (inutilizzato) la fine dell'operazione di I/O (**busy waiting**).

>[!note] Input Output **Interruzioni**
>- Modo più moderno di fare.
>- Il processore viene interrotto utilizzato soltanto quando il modulo I/O è pronto a scambiare i dati.
>- l processore salva il contesto del programma che stava eseguendo e comincia ad eseguire il gestore dell’interruzione.
>- Non c'è inutile attesa
>
>> **oss:** Quando il modulo di I/O è pronto il processore interrompe il processo che sta eseguendo e comincia a spostare le informazione dalla memoria del modulo io alla memoria principale (ram)

>[!note] Accesso Diretto in Memoria
>- È un sistema che permette ai dispositivi di I/O di leggere e scrivere direttamente dalla memoria principale.
>- DMA è um controller che gestisce il trasferenti diretto dei dati dalla memoria del dispositivo I/O alla memoria principale.
>- Il processore viene interrotto soltanto al termine del trasferimento.
>- Metodo più efficente.

## Multiprogrammazione

La multi programmazione è una tecnica che si basa sul idea che un processore deve poter eseguire più programmi contemporaneamente

>[!warning] oss
>1. La sequenza con cui i programmi sono eseguiti dipende dalla loro priorità e dal fatto che siano o meno in attesa di input/output.
>2. Alla fine della gestione di un’interruzione, il controllo potrebbe non tornare al programma che era in esecuzione al momento dell’interruzione.

## Gerarchie di memoria

>[!note] Gerarchia
>![[Pasted image 20240927140605.png|400]]

>[!warning] Andando verso il basso:
>- Diminuisce la velocità di accesso
>- Diminuisce il costo al bit
>- Aumenta la capacità
>- Diminuisce la frequenza di accesso alla memoria da parte del processore

>[!note] Memoria (primaria) Volatile
>- Le memorie volatili sono memorie che una volta persa l'alimentazione perdono i dati.
>- Sono molto pià veloci, ma hanno un costo per quantità di memoria estremamente più alto.

---
## Cache

> - La cache è una memoria molto piccola e molto veloce, contiene i dati utilizzati più spesso.

![[Pasted image 20240927141110.png|500]]

>[!warning] Info di Base
>- Cache anche se piccole hanno un grade impatto nel migliorare le performance di sistema
> - Il processore prima di accedere alla ram controlla se i dati che gli servono sono già all’interno della cache.
>- Serve mantenere consistenza tra **Cache** e **RAM**, questo vuol dire che ogni volta che un contenuto nella cache è modificato allora deve essere modificata anche la su "versione" in RAM.
>- La Cache è invisibile hai programmi compreso il sistema operativo, infatti è completamente gestita dall'hardware.

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

## Cache Gerarchica

Solitamente non esiste soltanto una cache all'interno della cpu ma ci sono i più cache alcune più piccole e veloci e altre più grandi ma più lente.

>[!note] Sistemi multi core
>Nei sistemi multicore, solitamente, è presente una o più cache per ogni core, e poi una cache generale.
>
>![[Pasted image 20240927150510.png|350]]

	