---
type: Uni Note
class: "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related:
completed: false
created: 2024-12-09T17:49
updated: 2026-01-31T13:32
---
>[!abstract] Related
>- [[Introduzione ai Sistemi Operativi]]
>- [[Sistemi Operativi 1 (class)]]

---
## Introduzione

Per implementare l'I/O ci sono principalmente 4 modalità, che sono riassunte da questa tabella:

|                             | **Senza Interruzioni** | **Con Interruzioni**           |
| --------------------------- | ---------------------- | ------------------------------ |
| **Passando per la CPU**     | I/O programmato        | I/O guidato dalle interruzioni |
| **Direttamente in Memoria** |                        | DMA                            |

>[!note] DMA
>
>- Il processo delega le operazioni di I/O al modulo DMA.
>- Il modulo trasferisce i dati direttamente da o verso la memoria principale
>- Quando l’operazione è terminata, il modulo genera l’interrupt per il processore
>  
>![[3. MOCS/Uni MOC/archive/attachments/Pasted image 20241209182918.png]]
>
>- ***Data Register:*** Contiene i dati da trasferire
>- ***Control Logic:*** Decide cosa deve fare, contiene quindi informazioni sull’operazione da eseguire.
>
>Le frecce che vanno verso l’esterno sono informazioni che il DMA da al S.O., le frecce verso di lui invece sono informazioni che riceve.

^ca893f

---
## Evoluzione della funzione di I/O

Nel tempo la gestione dell'input output si è evoluta:

>***1)*** Inizialmente era il *processore* a controllare i dispositivi periferici

>***2)*** Successivamente ad ogni dispositivo è stato introdotto un **modulo (controllore)** di I/O
>- I/O programmato, **senza interrupt**
>- Il processore non si occupa di tutti i dettagli del dispositivi periferici

>***3)*** Successivamente è stato introdotto il **modulo** (controllore) di I/O **con interrupt**
>- miglioramento dell’efficienza, il processore non deve aspettare che il dispositivo finisca l'operazione

>***4)*** Successivamente è stato implementato il [[#^ca893f|DMA]]
>- dati sono trasferiti direttamente tra dispositivo e memoria senza usare il processore
>- processore utilizzato soltanto all’inizio e alla fine dell’operazione.

>***5)*** Viene migliorato il [[#^ca893f|DMA]], il modulo I/O diventa un processore separato chiamato **I/O Channel**, successivamente gli viene data anche una **RAM dedicata**. Quindi molti dispositivi di ultima generazione sono dei “mini computer” a tutti gli effetti.

---
## Obbiettivi

Il sistema operativo ha degli obbiettivi specifici riguardanti la gestione dell I/O
- [[#Efficienza]]
- [[#Generalità]]

Per raggiungere questi obbiettivi è utilizzata la [[#Progettazione Gerarchica]]

---
### Efficienza

La maggior parte di dispositivi I/O sono molto più lenti rispetto alla RAM, proprio per questo la [[Introduzione ai Sistemi Operativi#Programmazione Singola e Multi Programmazione|Multi Programmazione]] è stata implementata in modo tale da sfruttare le pause dei programmi quando eseguono operazioni di I/O.

Ma questo non basta, infatti anche con l'utilizzo della multi programmazione c'è il rischio che il numero di processi che effettuano operazioni di I/O sia troppo alto e che la multi programmazione non tenga passo al processore.

È necessario quindi cercare soluzioni software dedicate a livello di S.O., come visto prima in particolare per il disco.

---
### Generalità

Esistono tantissimi tipi diversi di dispositivi di I/O, ma nonostante questo il sistema operativo deve fare del suo meglio per ***gestirli in modo uniforme***, nascondere la maggior parte dei dettagli dei dispositivi nelle operazioni a basso livello.

>[!example] Esempio
>
>Per richiedere accesso alle informazione contenute nel dispositivo utilizziamo la system call `read` indipendentemente dal tipo di dispositivo; quindi non esiste `read disk`, `read mouse`, `read ethernet`, ...

>***oss:*** Dobbiamo offrire diverse operazioni: `read`, `write`, `lock`, `unlock`, `open`, `close`.

---
## Progettazione Gerarchica

Si basa su un insieme di livelli dove: 
- ogni livello si basa su quello che fa il sottostante ed offre servizi al sovrastante
- ogni livello contiene funzionalità tra loro simili per complessità, tempi e astrazione. 

>***oss:*** modificare l'implementazione di livello non dovrebbe causare effetti sugli altri.


Ci sono 3 principali macro tipi di progettazione gerarchica:
- [[#^30b101|Dispositivo Locale]]
- [[#^70b855|Dispositivo di Comunicazione]]
- [[#^6793c9|File System]]

>[!note] Dispositivo Locale
>Usato per dispositivi locali, ad esempio stampante, monitor e tastiera.
>
>![[3. MOCS/Uni MOC/archive/attachments/Pasted image 20241210143858.png|150]]
>
>A ***livello più in alto*** abbiamo il *processo utente* che ha richiesto un’informazione da un dispositivo. 
>In ***fondo*** abbiamo l’*hardware* che fornisce istruzioni macchina.
>
>In ***mezzo*** abbiamo le operazione effettuare tal sistema operativo:
>- **logical I/O**: Da un’interfaccia logica al programma, l’utente quindi può chiedere di fare queste istruzioni. Lui le trasforma e le passa a
>- **Driver I/O**: Trasforma le richieste logiche in comandi I/O.
>- **Scheduling and Control**: Invia le vere e proprie richieste in linguaggio macchina>

^30b101

>[!note] Dispositivo di Comunicazione
>I dispositivi di comunicazione come schede ethernet e wifi funzionano in modo simile ai [[#^30b101|dispositivi locali]] ma al posto di ***Logical I/O*** abbiamo **Communication Architecture**.
>
>Questo perché possiamo avere diverse architetture di comunicazione, ad esempio TCP/IP.
>
>![[3. MOCS/Uni MOC/archive/attachments/Pasted image 20241210144958.png|140]]

^70b855

>[!note] File System
>
>Struttura organizzativa utilizzata per dispositivi di storage dati come *HDD*, *SDD*, *USB Key*, *CD*, ...
>
>![[3. MOCS/Uni MOC/archive/attachments/Pasted image 20241210145425.png|140]]
>
>Anche qui partiamo da processo utente e arriviamo all’hardware.
>- **Directory Management**: Definisce le operazioni sui file come crearli, cancellarli ecc…
>- **File System**: È la struttura logica dell’operazione quindi come dobbiamo aprirli, scriverli ecc…
>- **Organizzazione Fisica**: Si occupa di allocare e deallocare spazio sul disc

^6793c9

