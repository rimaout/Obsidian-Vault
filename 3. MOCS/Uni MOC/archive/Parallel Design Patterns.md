---
type: Uni Note
class:
  - "[[Programmazione Sistemi Multicore (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-10-21T17:31
updated: 2025-11-04T18:06
---
## Parallel Design Patterns

Sono dei [[design pattern]] ma applicati alla programmazione parallela, ovvero dei modi per risolvere problemi comuni incontrati nella programmazione parallela. Ne esistono di due principali tipologie:
- [[#Globally Parallel, Locally Sequential (GPLS)]]
- [[#Globally Sequential, Locally Parallel (GSLP)]]

![[Pasted image 20251103150451.png|600]]

## Globally Parallel, Locally Sequential (GPLS)

L'applicazione esegue parallelamente diversi task (sequenziali), alcuni design patter di questo tipo sono:

>[!note] Single-Program, Multiple Data
>
>Tutta la logica dell'applicazione è mantenuta in un singolo programma.
>
>Solitamente la struttura del programma è:
>1. Inizializzazione del programma
>2. Ottenimento degli identificatori
>3. Esecuzione del programma in diverse ramificazioni in base ai core coinvolti (parte parallela)
>4. Terminazione del programma
>   
>***Down sides***: questo design pattern non può essere utilizzato quando:
>- requisiti di memoria troppo alti
>- nodi di piattaforme diverse (non tutti uguali)
>
>Questi problemi sono risolti da: [[#^6aeff1|Multiple-Program Multiple Data]] design patern.

^a2d304

>[!note] Multiple-Program Multiple Data
>
>Ha gli stessi step di [[#^a2d304|Single-Program, Multiple Data]] ma il carico è suddiviso so più programmi che comunicano tra loro, e che lavorano su dati anche diversi.
>
>>***Nota:*** programmi possono essere eseguiti anche su piattaforme diverse.

>[!note] Master-Worker
>
>Design pattern che suddivide i processi/thread in due compiti:
>- **Master**: un processo o thread che suddivide il problema in task, li distribuisce ai worker, raccoglie i risultati parziali e si occupa dell'I/O principale e dell'interfaccia utente.    
>- **Worker**: più processi o thread che ricevono compiti dal master, li eseguono e restituiscono i risultati. I worker, una volta completato un task, chiedono subito il successivo al master, massimizzando l'uso delle risorse.
>
>>**Load balancing Implicito**: I worker più veloci eseguono più task, minimizzando i tempi morti.
>
>>**Master collo di bottiglia**: il master può saturare facilmente se i task sono troppo piccoli o il numero di worker è molto alto, per ridurre ridurre questo problema si utilizza una *gerarchia di master*.

>[!note] Map-Reduce
>
>Una versione modificata di Master-Worker, in cui i nodi worker eseguono due tipi di operazioni:
>- **Map**: Esegue la computazione su un insieme di dati che risulta in un insieme di risultati parziali (ad esempio, esegue la somma su ogni elemento di un vettore)
>- **Reduce**: Colleziona i risultati parziali e ne deriva un risultato finale (ad esempio, somma tutti gli elementi di un vettore ottenendo un unico scalare)
>

## Globally Sequential, Locally Parallel (GSLP)

L'applicazione è composta da uno specifico "flusso" di esecuzione sequenziale, di cui alcune parti vengono eseguite in parallelo.

>[!note] Fork/Join
>
>C'è un unico "padre" in cui parte l'esecuzione seriale, i figli sono creati attraverso una `fork` quando ce ne è bisogno, per eseguire le parti parallele, una volta che un figlio termina l'esecuzione viene "distutto".
>
>>***Nota:*** creare e distruggere un thread è costoso, quindi nella pratica i figli vengono creati e poi quando hanno finito sono messi in idle, e se c'è un nuovo lavoro può essere assegnato ad uno di questi figli.
>
>**Esempio** il fork join può tornare utile quando abbiamo problemi ricorsivi, ad esempio:
>
>```c
>mergesort(A, lo, hi):
>	if lo < hi:                     // at least one element of input
>		mid = ⌊lo + (hi - lo) / 2⌋
>		fork mergesort(A, lo, mid)  // process (potentially) in
>								    // parallel with main task
>		mergesort(A, mid, hi)       // main task handles
>									//second recursion
>		join
>		merge(A, lo, mid, hi)
>```

>[!note] Loop Parallelism
>
>Risulta estremamente semplice da utilizzare e viene spesso applicata quando un programma sequenziale deve essere adattato al multiprocesso. Consiste nel parallelizzare ogni esecuzione di un ciclo for , è necessario che le iterazioni però siano indipendenti fra loro.
>
>>***Nota:*** è la stessa cosa che hai fatto con il progetto python per la conversione da `flac` a `mp3`: [flac2mp3](https://github.com/rimaout/flac2mp3)
