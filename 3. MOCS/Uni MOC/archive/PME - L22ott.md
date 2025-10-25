---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2025-10-21T17:31
updated: 2025-10-21T18:42
---
## Parallel Design Patterns

Sono dei [[design pattern]] ma applicati alla programmazione parallele, ovvero dei modi per risolvere problemi comuni incontrati nella programmazione  parallela, ci sono due principali tipologie:
- Globally Parallel, Locally Sequential (GPLS)
- Globally Sequential, Locally Parallel (GSLP)

## Globally Parallel, Locally Sequential (GPLS)



>[!note] Multiple Program Multiple Data
>
>Single Program Multiple Data fallisce quando ...
>
>MPMD ha più eseguibili gh

>[!note] Master-Worker
>
>Quando un nodo finische il lavore ne riceve uno nuovo, quindi più il nodo è efficente più lavora
>
>il nodo master deve rischia di essere un bottleneck, molto spesso si usa una gerarchia di master per suddividere il lavoro e non avere un unico punto di fallimento

>[!note] Map-Reduce
>
>Non è detto ci sono entrambe, a volte ce solo reduce e a volte solo map
>
>la principale differenza dal master e worker è che 
## Globally Sequential, Locally Parallel (GSLP)

>[!note] Fork/Join
>
>In questo modello c'è un processo padre da cui parte l' esecuzione, i figli sono creati ad esecuzione quando ce ne è bisogno.
>
>Creare e distuggere un theread è costodo, quindi nella pratrica  i thread vengono creati e poi quanfdo hanno finito sno messi in idele, e se c'è un nuovo lavoro può essere assegnato ad uno idele.
>
>
>Torna utile quando abbiamo problemi ricorsivi ad esempio:
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
>Molto utilizzato per la sua semplicità e efficacia, naturalmente è utile soltanto in casi specifici in cui si hanno dei loop ...

Fai esercizio trapezio

## Input

è convenzione che la gestione dell’input sia fatto dal processo (rank)

Inoltre molte implementazioni di MPI permettono soltanto al rank 0 di leggere lo `stdin`, ad esempio se dobbiamo utilizzare una `scanf` (ovvero leggere lo stdin) deve essere fatta dal rank 0.

Esempio di lettura user input:

![[Pasted image 20251021182436.png|800]]

in realtà non è un ottima implementazione, infatti in MPI c'è un modo ufficiale per fare una broadcast (ovvero un nodo che comunica a tutti gli altri un informazione). Inoltre c'è un altro problema ovvero vengono fatte due MPI_Send di due double consecutivamente, potevano essere raggruppate in un unica send.

## Collettive

Vedremo le collettive già implementate in MPI


>[!note] Reduce
>
>È un operazione di riduzione a cui fa specificata un operazione (es. somma, massimo, media ...)
>
>Firma:
>
>- vettore in input
>- vettore in uscita
>- ...
>- Processo di destinazione


