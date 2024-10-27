---
type: Uni Note
class:
  - "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related: "[[Interruzioni 101]]"
completed: true
created: 2024-10-26T10:56
updated: 2024-10-27T15:07
info: 
---
>[!abstract] Index
>1. [[#Thread in Linux]]
>2. [[#Processi Proces Control Block (PCB) PCB in Linux|PCB in Linux]]
>3. [[#Stati dei Processi Linux]]
>4. [[#Segnali ed Interrupt in Linux]]

>[!abstract] Related
>- [[Sistemi Operativi 1 (class)]]
>- [[Interruzioni 101]]

---
## Thread in Linux

Linux, nonostante sia un sistema operativo moderno, non si comporta come visto in [[Thread#Rappresentazione dei Threads|Rappresentazione dei Threads]], questo perché è basato su Unix e Unix non prevedeva l'utilizzo di thread. Quindi in Linux è stato implementato il funzionamento dei thread con alcuni vincoli dettati dall'architettura di Unix.

>[!note] Caratteristiche dei threads in linux
>
Il kernel Linux non fa una distinzione netta tra processi e thread, ma piuttosto considera i thread come processi che condividono alcune risorse (come la memoria e i file descriptor) con altri thread dello stesso gruppo.
>
>I thread sono chiamati **LWP** (Lightweight Process) 
>
>Esistono sia i **[[Thread#ULT vs KLT|KLT (kernel level threads)]]** che gli **[[Thread#ULT vs KLT|ULT (user level threads)]]** ma:
>- KLT sono usati principalmente del sistema operativo
>- ULT possono essere scritti da qualsiasi utente, poi solitamente vengono convertiti in KLT (esempio se si usa la libreria `pthreads`)

>[!note] Identificazione dei Thread
>Ogni Thread (LWP), proprio come i processi, ha il proprio [[Processi#Proces Control Block (PCB)|PCB (process control block)]], e in quest’ultimo sono presenti tutte le informazioni necessarie per la gestione dei thead.
>
>In particolare per quanto riguarda gli identificatori abbiamo:
>- il **TGID** (thread group leader identifier) è un identificatore unico per tutti i thread appartenenti ad uno stesso processo, e non è altro che il *PID* (process identifier) del processo a cui appartengono i therad.
>- il **TID** (task identifier) è un identificatore univoco per ogni thread di un processo, a volte viene chiamato anche *PID* (process identifier) del thread (in linux non c'è una netta distinzione tra thread e processi).
>
>Il *TID* del primo thread creato da un processo coincide con il *PID* del processo che lo ha creato, questo vuol dire che in processi con un solo thread il *TID* e il *TGID* coincidono.
>
>>[!tip] Comandi Linux
>>- Il comando `getpid()` restituisce il *TGID*
>>- Il comando `ps` in Linux è utilizzato per visualizzare le informazioni sui processi in esecuzione sul sistema, per quanto riguarda i Thread il *TGID* è sotto il nome di PID e *TID* sotto nome di TID o SPID o LWP.

---
### [[Processi#Proces Control Block (PCB)|PCB]] in Linux

Questa è la rappresentazione ad alto del [[Processi#Proces Control Block (PCB)|PCB]] in Linux

![[Pasted image 20241027111758.png|500]]

>[!info] 
>Nel [[Processi#Proces Control Block (PCB)|PCB]] di linux è possibile trovare sia il **TID** che il **TGID**, Le frecce indicano i puntatori, a delle strutture esterne al PCB. 
>
>Il puntatore a **thread info**, contiene diverse informazioni a basso livello, tra cui questa il _kernel stack_, ovvero lo stack che contiene le chiamate per il codice di sistema (esempio le system call).
>
>>[!caption|right]
>> 
>>![[Pasted image 20241027144151.png|400]]
>
>Nell’immagine non è riportato ma c’è un puntatore **thread group (lista concatenata)** che ci permette di rintracciare gli altri thread dello stesso processo.
>
>I puntatori **parent e real_parent** puntano al padre del processo e ci sono puntatori simili anche per **fratelli e figli**.

---
## Stati dei Processi Linux

In Linux il modello degli stati è molto simile al [[Processi#Modello a 5 Stati|modello a 5 stati]], visto precedentemente -

Tuttavia ci sono degli stati "atipici" rispetti al [[Processi#Modello a 5 Stati|modello a 5 stati]]:
- Non è presente lo stato `suspended`, questo significa che un processo può essere sospeso ma non per scelta dell'OS.
- `TASK_RUNNIG`: non è presente la distinzione tra sia *Ready* che *Running*.
- `TASK_INTERRUPTIBLE`, `TASK_UNINTERRUPTIBLE`, `TASK_STOPPED`, `TASK_TRACED`: sono tutti **Blocked** ma differiscono per il motivo per cui il processo è stato bloccato.
- `EXIT_ZOMBIE` e `EXIT_DEAD`sono entrambi Exit

---
## Segnali ed Interrupt in Linux

>[!note] Segnali
> I Segnali possono essere inviati da un processo utente ad un altro processo utente tramite system call.
>
>>**oss:** questa system call, in modo contro intuitivo, si chiama `kill` anche se non è utilizzata soltanto per terminare un processo.
>
>Quando un segnale viene inviato ad un processo allora viene aggiunto nella sezione dei `signal pending` nel [[#Processi Proces Control Block (PCB) PCB in Linux|PCB]] del processo che ha ricevuto il segnale. Questa non è altro che una coda dei segnali da eseguire.
>
>Quando è arrivato il momento una funzione chiamata **Signal Handler** prenderà il carico il segnale. 

>[!note] Signal Handler
>I **Signal Handler** sono delle funzioni che si occupano ricevuti da un processo.
>
>I Signal Handler di sistema possono essere sovrascritti da dei signal handler definiti dal programmatore 
>- oss: alcuni signal hanno degli handler che non possono essere sovrascritti
>
>Tutti i **Signal Handler** sono eseguiti in *user mode*, al contrario degli **Interrupt Handlers**, che gestiscono le interruzioni, sono eseguiti in *kernel mode*.


>[!warning] Casi Particolari
>I segnali possono essere anche inviati da un processo che si trova in modalità sistema, spesso però se accade significa che sia dovuto ad un interrupt a monte, _esempio_:
   > 
>Eseguiamo un programma C scritto male, che accede ad una zona di memoria senza averla richiesta. Viene generata un’eccezione, successivamente viene eseguito il corrispondente handler in modalità kernel che manda un segnale `SIGSEGV` al processo colpevole.
   > 
> La prossima volta che verrà mandato in esecuzione il processo il kernel vedrà dal PCB che c’è un segnale in attesa ed eseguirà l’azione corrispondente, di default è la terminazione del processo ma l’utente può riscriverla, in ogni caso questa azione è eseguita in **modalità utente**. Ovviamente per la terminazione viene chiamata un’altra syscall che verrà eseguita in modalità kernel.