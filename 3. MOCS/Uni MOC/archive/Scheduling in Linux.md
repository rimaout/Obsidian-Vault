---
type: Uni Note
class:
  - "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related:
  - "[[Scheduling]]"
  - "[[Scheduling in UNIX]]"
completed: true
created: 2024-11-07T12:31
updated: 2026-01-31T13:32
---
>[!abstract] Related
>- [[Scheduling]]
>- [[Scheduling in UNIX]]
>- [[Sistemi Operativi 1 (class)]]

---
## Introduzione

Lo scheduler Linux è derivato dallo [[Scheduling in UNIX|scheduler Unix]], con alcune differenze tali che permettono di ottenere un alta velocità di esecuzione, raggiunta tramite semplicità di implementazione.

---
## Caratteristiche

>[!note] Durata di Sheduling
>Proprio per raggiungere elevate prestazione e semplicità di implementazione non si utilizzano [[Scheduling (Introduzione)#Tipi di Scheduling|long-term o medium-term scheduling]].
>
>In realtà in rari casi quando non c'è abbastanza memoria da allocare per un nuovo processo, si utilizza una sorta di long-term scheduling che si assicura che il nuovo processo non venga creato.

>[!note] Code
>Ci sono due tipi di code:
>- wait-queues
>- run-queues
>
>Le **wait-queues** (suspended) sono le code in cui i processi sono messi in attesa, dopo aver fatto una richiesta che implichi l'attesa (es. richiesta di I/O)
>
>Le **run-queues** (ready) sono le code da cui il [[Scheduling (Introduzione)#Short-Term Scheduling (dispatcher)|dispatcher]] sceglie i processi da eseguire.
>
>>**oss:** in [[Scheduling in Architetture Multiprocessore|architetture multi processore]] le wait-queues sono condivise tra i processori, invece ogni processore ha le proprie run-queues.

>[!note] Decision Mode & Priority
>Come in unix, lo scheduler linux utilizza un [[Algoritmi di Scheduling|algoritmi di scheduling]] con:
>- Modalità di decisione [[Algoritmi di Scheduling#^363dc9|Preemptiv]]
>- Probabilità **Dinamica**
>  
>Con probabilità dinamica si intende che la probabilità che un processo:
>- aumenta man mano che i processo è in attesa di essere eseguito
>- diminuisca man mano che il processo è in esecuzione

---
## Rapidità d'esecuzione

Lo scheduler linux ha importanti correzioni che gli permettono di:
- essere veloce e di operare in quasi $O(1)$
- servire in modo appropriato i processi real-time

>[!warning] Come?
> Lo **scheduler** viene attivato da un interrupt ogni *1 ms*. Valore ottima infatti se si sceglie un intervallo:
> - **minore** il sistema operativo viene eseguito troppo spesso rispetto al processi user.
> - **lungo** ci sono problemi per i processi real-time.
>   
>Il fatto che lo scheduler venga eseguito ogni 1 ms implica che i processi vengano eseguiti per un quanto di tempo `multiplo` di 1 ms. Il valore di questo `multiplo` dipende dal tipo di processo:
>
>- **Interattivi:**
>    - Da quando è avvenuta l'interazione con programma bisogna eseguirli in CPU entro 150ms (altrimenti l'utente può percepire rallentamenti)
>- **Batch:**
>    - Sono penalizzati dallo scheduler, infatti l’utente non dovendo usare il programma attivamente non ricerca reattività
>- **Real Time:**
>    - I 2 tipi precedenti vengono individuati da Linux in modo autonomo tramite dei suoi metodi, per questo tipo di processi invece deve essere presente la system call `sched_setscheduler` nel codice sorgente.
>    - Normalmente sono utilizzati solo dai KLT (Kernel Level Thread) di sistema.

---
## Classi di Scheduling

Ci sono principalmente 3 classi di scheduling:

- **SCHED_FIFO** per processi *real-time*
- **SCHED_RR** (round robin) per i processi *real time*
- **SCHED_OTHER** (round robin) per tutti gli altri

>[!note] Livelli di priorità
>
>Prima si eseguono i processi con scheduler SCHED_FIFO e SCHED_RR, poi con SCHED_OTHER:
>
>- **SCHED_FIFO** e **SCHED_RR** hanno priorità da *1 a 99*, mentre **SCHED_OTHER** ha priorità da *100 a 139*.
>
>Ogni processore ha *140 run-queues*, una per ogni livello di priorità (da 0 a 140). La priorità di livello 0 è utilizzata per casi speciali.
>
>Lo scheduler inizia a cercare processi da eseguire nella coda di livello 0 e aumenta progressivamente il livello, passando dal livello $n$ al livello $n+1$ solo se:
>   - Non ci sono processi in $n$ 
>   - Nessun processo in $n$ è in stato di _RUNNING_ (ready).

>[!note] Preemption
>Come detto la modalità di decisione dello schedulerè [[Algoritmi di Scheduling#^363dc9|Preemptiv]], in questo caso lo scheduler può bloccare un processo in esecuzione per eseguirne un altro per 2 emotivi:
>1. Se il processo in esecuzione ha esaurisce il suo quanto di tempo.
>2. Se un altro processo ad alta priorità passa da uno stato _blocked_ a _RUNNING_ (ready).
>
>Il secondo caso, è molto comune quando un processo **interattivo** ha cambiato stato da blocked a ready e quindi deve essere eseguito 150ms. In queste situazioni un processo in esecuzione può essere interrotto dallo scheduler per essere sostituito da un processo interattivo.
>
>Questo però non vale per i processi SCHED_FIFO infatti:
>
>>[!warning] SCHED_FIFO
>>Un processo SCHED_FIFO viene rimosso dall'esecuzione soltanto se:
>> - si blocca per I/O
>> - rilascia volontariamente la CPU
>> - se un altro processo ad alta priorità passa da uno stato _blocked_ a _RUNNING_ (ready).
>>
>>Quindi i processi SCHED_FIFO **non sono limitati dai quanti di tempo**.
>
>I processi real-time **non cambiano mai priorità** mentre gli **SCHED_OTHER** si, ovvero man mano che vanno in esecuzione la loro priorità decresce.
