---
type: Uni Note
class:
  - "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2024-10-04T18:51
updated: 2025-08-21T17:49
---
>[!abstract] Related
>- [[Sistemi Operativi 1 (class)]]

---
## Introduzione

Uno dei compiti principali dei sistemi operativi è la **gestione dei processi**, in particolare un sistema operativo deve permettere:
- Esecuzione alternata di processi multipli (**interleaving**).
- Assegnare le risorse ai processi, e proteggere dagli altri processi.
- Scambio di informazioni tra processi.
- Sincronizzazione dei Processi.

>[!note] Processo (definizione)
>Si tratta di un'istanza di un programma in esecuzione, ed è composto da:
>- Codice (anche condiviso).
>- Un insieme di dati.
>- Attribbuti che descrivono lo stato del processo.

>[!note] Trace (definizione)
>Il comportamento di un particolare processo è caratterizzato dalle sequenza di istruzioni che vengono eseguite, questa sequenza è chiamata **Trace** (traccia).

>[!note] Dispatcher (definizione)
>Il **Dispatcher** è un piccolo programma è fa parte del sistema operativo (è in memoria kernel) che si occupa di sospendere un processo per eseguirne un altro.

---
## Attributi 

Finche un processo è in esecuzione, ad esso sono associate delle informazioni, tra le quali:
- PID (Process Identifier - per distinguerlo da altri processi)
- [[#Stati Base|Stato]] 
- Priorità 
- Hardware Context (valore corrente dei registi della CPU, compreso program counter)
- Puntatori a Memoria (immagine del processo)
- Stato dell'I/O
- Informazioni di accounting (utente che sta eseguendo il processo)

---
## Stati di un Processo

#### Stati di Base

Un processo ha 4 possibili stati `creazione`, `running`, `not running` e `terminazione`.

>[!warning] Creazione
>
>In ogni istante in un sistema operativo c'è sempre almeno un processo in esecuzione, e tra questi c'è sempre almeno un interfaccia utente, utilizzata per l'avvio di nuovi processi.
>
>Questa "tecnica" è chiamata **Process Spawning**, ovvero quando un processo crea un altro processo.
>- Il processo che crea il nuovo processo è detto `processo padre`.
>- Il processo generato è detto `processo figlio`. 
>
>>**oss:** Il vecchio processo resta in esecuzione, quindi si passa da $n$ processi ad $n + 1$ processi.

>[!warning] Esecuzione (running & not running )
>Quando un processo è attivo (in esecuzione) , può avere due stati:
>- **running:** ovvero che il processore sta eseguendo le istruzioni del processo.
>- **not running:** ovvero che sta aspettando il suo turno per essere eseguito da processore.
>  
>  ![[Pasted image 20241005150610.png|400]]
>>**oss:** Questa immagine rappresenta una cosa per un [[#Modello a 2 Stati]].

>[!warning] Terminazione
>Ci sono due tipi di terminazioni:
>
>1. La **Terminazione Prevista:** che può avvenire perché il processo ha terminato il suo scopo e si "chiude" in automatico, o voluta dall'utente che "chiude" in modo controllato il processo. 
>2. La **Terminazione NON Prevista:** che può avvenire per l’esecuzione di un istruzione non consentita, che richiede l'intervento del sistema operativo per la "chiusura" forzata del processo.
>   
>>**oss:** Esistono anche processi che rimangono sempre in esecuzione.
>
>Esistono altre due classificazioni per descrivere il tipo di terminazione:
>1. **Completamento** del processo: processo raggiunge la fine delle sue istruzioni (ultima istruzione è `HALT`ed genera un’interruzione per il SO)
>2. **Uccisione** del processo dovuta da:
>	- Intervento del OS per errori (esaurimento memoria, acceso area protetta, I/O fallita ...)
>	- Utente (chiudere una finestrata)
>	- Da un altro processo
>
>>**Processo Master:** C'è sempre un processo master che non può essere terminato.

#### Modello a 2 Stati

![[Pasted image 20241006104411.png|450]]

>[!note] Implementazione a 1 coda
>
>![[Pasted image 20241005150610.png|400]]

#### Modello a 5 Stati

![[Pasted image 20241005154848.png|450]]

>[!warning] Osservazioni 
>- Quando un nuovo processo è creato non va subito in esecuzione (va in ready)
>- In questa immagine non è rappresentato ma si può passare anche ready o blocked ad exit (un processo ne kill un altro)

>[!note] Implementazioni a 2 o più code
>
>![[Pasted image 20241005154908.png|450]]
>![[Pasted image 20241005154929.png|450]]
>
>Nell'implementazione a più code, ad ogni coda sono assegnati processi che sono bloccati per motivi specifici (coda di attesa I/O da memoria, coda di attesa Input da utente ...)
>
>Questo permette di essere più efficienti, perché quando si verifica un interrupt che comunica al processore che un determinato evento è avvenuto, il processore può andare direttamente alla coda associata a quell'evento e avviare il primo processo che è possibile eseguire. Ciò permette di non dover cercare in tutte le code.
#### Modello con Stati Sospesi

Quando il processore è principalmente inutilizzato o la memoria principale è sovraccarica si possono spostare i processi in attesa dalla memoria principale al disco, cosi da liberare memoria e non lasciare il processore inoperoso. 

- Questi tecnica è chiamata sospensione dei processi.
- L'azione di spostare un processo dalla RAM ad un disco è chiamata `memory swap`.
- Il processo che è stato spostato dalla RAM al disco e detto sospeso.

**Casi di Sospensione:**

| Motivo                       | Info                                                                                                                                  |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| Swapping                     | Il SO ha bisogno di rilasciare abbastanza memoria da portarci dentro un processo ready                                                |
| Interno al SO                | Il SO sospetta che il processo stia causando problemi                                                                                 |
| Richiesta utente interattiva | Ad esempio: debugging, o correlato all’uso di<br>una risorsa                                                                          |
| Periodicità                  | Il processo viene eseguito periodicamente può venire sospeso in attesa della prossima esecuzione                                      |
| Richiesta del padre          | Il padre potrebbe voler sospendere l’esecuzione<br>di un figlio per esaminarlo o modificarlo, o per coordinare l’attivi tra più figli |

>[!note] Uno Stato Sospeso
>![[Pasted image 20241006110155.png|450]]

>[!note] Due Stati Sospesi
>![[Pasted image 20241006110217.png|450]]
>
>Naturalmente il dispatcher esegue soltanto i processi `ready` e non i `ready/suspended`.

^458367897

---
## Condivisione delle Risorse

Il sistema operativo ha il compito di distribuire le risorse tra i pari processi per fare ciò si basa su delle tabelle

>[!note] Tabelle di Memoria
>Le tabelle di memoria sono usate per gestire sia la memoria principale che quella secondaria (secondaria che serve per la memoria virtuale)
>
>Devono comprendere le seguenti info:
>- allocazione di memoria principale da parte dei processi
>- allocazione di memoria secondaria da parte dei processi
>- attributi di protezione per l’accesso a zone di memoria condivisa
>- informazioni per gestire la memoria virtuale

>[!note] Tabelle per I/O
>Usate dal SO per gestire i dispositivi e i canali di I/O 
>
>Il SO deve sapere:
>- se il dispositivo è disponibile o già assegnato
>- lo stato dell’operazione di I/O
>- la locazione in memoria principale usata come sorgente o destinazione del trasferimento di I/O

>[!note] Tabelle dei File
>Queste tabelle forniscono informazione su: 
>- esistenza di files
>- locazioni in memoria secondaria
>- stato corrente
>- altri attributi
>
>Memorizzate parte su disco e parte in RAM

>[!note] Tabelle dei Processi
>Tabella che continente le informazioni di ogni processo necessarie per la gestione dei processi
>
>In particolare:
>- [[#Stati Base|Stato]]
>- Proces Identifier (PID)
>- [[#^32425234|Process Control Block (PCB)]] contenete gli [[#Attributi]] di ogni processo
>- [[#^32445657643|Proces Image]]

>[!warning] Process Image
>L’insieme di programma sorgente, dati, stack delle chiamate e [[#^32425234|PCB]]

^32445657643

---
## Stato del Processore

È la rappresentazione del contenuto di tutti i registri del processore in un certo instante.

---
## Proces Control Block (PCB)

Contiene informazioni di cui il SO ha bisogno per controllare e coordinare i vari processi attivi
- Salvate nella zona riservata al [[Kernel]] (accessibile soltanto all'OS).
- Contiene gli [[#Attributi]] del processo.
- Permette la gestione di più processi, ovvero contiene sufficienti informazioni per bloccare un programma in esecuzione e farlo riprendere più tardi dallo stesso punto in cui si trovava.

>[!note] Informazioni
>
>>[!column|flex]
>>
>>>[!note|clean no-t]
>>>
>>>**Identificatori:**
>>>- del processo (PID) 
>>>- del processo padre (Parent PID, o PPID)
>>>- dell’utente proprietario
>>>  
>>>**Informazioni sullo stato del processore:**
>>>- registri utente (accessibili in linguaggio macchina/assembler) 
>>>- program counter 
>>>- stack pointer
>>>- registri di stato: risultati di operazioni aritmetico/logiche
>>>- modalità di esecuzione, interrupt abilitati/disabilitati
>>>  
>>>**Informazioni per il controllo del processo:**
>>>- stato del processo (ready, suspended, blocked, ...) 
>>>- priorit`a 
>>>- informazioni sullo scheduling (ad es.: per quanto tempo `e stato in esecuzione l’ultima volta)
>>>- l’evento da attendere per tornare ad essere ready, se attualmente in attesa
>>>
>>>**Supporto per strutture dati:**
>>>- puntatori ad altri processi 
>>>- per mantenere liste concatenate di processi nei casi in cui siano necessarie (es., code di processi per qualche risorsa)
>>>
>>>**Comunicazioni tra processi:** flag, segnali, messaggi per supportare comunicazioni tra processi
>>>
>>>**Permessi speciali:** non tutti i processi possono accedere a tutto
>>>
>>>**Gestione della memoria:** puntatori ad aree di memoria che gestiscono l’uso della memoria virtuale
>>>
>>>**Uso delle risorse:** file aperti uso di risorse (compreso il processore) fino ad ora
>>>
>>
>>>[!caption]
>>> 
>>>![[Pasted image 20241004194346.png|170]]

^32425234

---
## Modalità di Esecuzione dei Processi

La maggior parte dei sistemi operativi supporta due modalità di esecuzione:
- [[#^fc38aa|Modalità Kernel]]
- [[#^5571a8|Modalità Utente]]
  
I processori possono avere altre modalità di esecuzione, ma sistemi operativi come Linux utilizzano soltanto le corrispettive modalità kernel e utente.
  
>[!note] Modalità **[[Kernel]]**
>Modalità (senza limitazioni) che permette di avere il pieno controllo sulla macchina 
>  
> Operazioni possibili:
> - Gestione dei processi (creazione, scheduling, sincronizzazione, comunicazione)
> - Gestione della memoria (allocazione per i processi, gestione memoria virtuale)
> - Gestione dell I/O (assegnazione delle risorse ha processi, gestione buffer e cache)
> - Funzioni di supporto (gestione interrupt, accounting, monitoraggio)
>   
>Esempio di operazioni possibili:
>- permette di accedere a qualsiasi locazione di memoria 
>- permette di eseguire istruzioni che bloccano gli interrupt

^fc38aa

>[!note] Modalità Utente
>Modalità (con limitazioni) dove molte operazioni sono vietate, quindi per poter eseguire determinate operazioni (esempio operazioni di I/O) si ha il bisogno di passare un processo alla kernel mode.
>
>1. Prima di tutto un processo utente inizia sempre in modalità utente
>2. Per passare da modalità utente a kernel il processo viene interrotto da un interrupt
>3. L'hardware cambiamo la modalità di esecuzione del processo (da utente a kernel)
>4. Viene eseguito un Interrupt Handler (istruzioni facente parti del kernel)
>5. Il processo ora attraverso l'Interrupt Handler po eseguire le operazioni del kernel
>6. Poi come ultima operazione l'Interrupt Handler ripristina la modalità di esecuzione del processo a modalità utente
>   
>>**oss:** Quando un processo va in modalità kernel può eseguire soltanto istruzioni presenti nel kernel stesso (software di sistema) e non comandi scritti nel suo codice sorgente.

^5571a8

L’interrupt handler può essere eseguito in diversi “modi”, e in tutti questi dobbiamo essere in kernl mode.

Eseguito per conto dello stesso processo interrotto che lo ha esplicitamente voluto
- System calls oppure in risposta ad una sua richiesta di I/O

Eseguito per conto dello stesso processo interrotto ma non voluto:
- Errore fatale (_abort_): Il processo viene terminato
- Errore non fatale (_fault_): Trasparente rispetto al processo

Codice eseguito per conto di un altro processo
- È un caso particolare dove ad esempio un processo _A_ ha fatto richiesta di I/O e si trova adesso in stato _blocked_, se durante l’esecuzione di un altro processo _B_ viene eseguita la richiesta di _A_ allora l’interrupt viene eseguito per conto del processo _B_ ma è in risposta a quello che ha chiesto _A_. Questo è ormai “accettato” nei moderni sistemi operativi.

---
## Creazione di un Processo

Il Sistema Operativo deve:
- Assegnargli un [[PID]]
- Allocargli spazio in [[Memoria Principale (RAM)]]
- Inizializzare il [[#Proces Control Block (PCB)]]
- Inserire il processo nella giusta coda ([[#Stati di un Processo]])
- Creare o espandere strutture dati come ad esempio quelle per l’accounting

---
## Switching tra Processi

Con switching si intendo l'azione di sostituire un processo in esecuzione con un altro che era in uno stato di attesa.


**Quando viene effettuato uno switch di processo:**

| Meccanismo     | Causa                                             | Uso                                                                                 |
| -------------- | ------------------------------------------------- | ----------------------------------------------------------------------------------- |
| Interruzione   | Esterna all’esecuzione dell’istruzione corrente   | Reazione ad un evento esterno asincrono; include i quanti di tempo per lo scheduler |
| Eccezione      | Associata all’esecuzione dell’istruzione corrente | Gestione di un errore sincrono                                                      |
| Chiamata al SO | Richiesta esplicita                               | Chiamata a funzione di sistema (caso particolare di eccezione)                      |

  
>[!note] Passaggi per switching fra processi
>
>Ricordiamo che vanno tutti eseguiti in Kernel Mode
>
>1. Salvare il contesto del programma ovvero registri e PC (copiati nel [[#Proces Control Block (PCB)|PCB]])
>2. Aggiornare il [[#Proces Control Block (PCB)|PCB]] attualmente in esecuzione
>3. Spostare il [[#Proces Control Block (PCB)|PCB]] nella [[#Stati di Base|coda]] appropriata
>4. Scegliere un altro processo da eseguire
>5. Aggiornare il [[#Proces Control Block (PCB)|PCB]] del nuovo processo
>6. Aggiorna le strutture dati per la gestione della memoria
>7. Ripristina il conteso del processo (registri)

---
## Esecuzione dell'OS?

Il Sistema Operativo è un insieme di programmi ed è eseguito dal processore come ogni altro programma. Molto spesso lascia che altri programmi vadano in esecuzione per poi riprendere il controllo tramite gli interrupt.

>[!question] L'OS è un processo?
>È facile notare che il sistema operativo (OS) si comporta in modo simile ad altri programmi, quindi è facile pensare che sia un processo come gli altri. Tuttavia, la risposta non è così semplice. In realtà, esistono diversi tipi di sistemi operativi e diversi modi in cui vengono eseguiti."

### Kernel Separato

> [!caption|right]
>
>![[2010241444.png]]

Il Kernel viene eseguito al di fuori dei processi, quindi in questo caso il sistema operativo **non è un processo**. Questo è **eseguito come entità separata** con privilegi elevati e zone di memoria riservate.

### Kernel Interno ai Processi Utente

^1fa6c4

> [!caption|right]
>
>![[2010141445.png]]

In questo caso il Sistema Operativo viene eseguito nel contesto di un processo utente dopo un interrupt. Come visto prima questo interrupt è una parte del SO che viene eseguita e “delegata” al processo in esecuzione.

**Comunque lo stack delle chiamate del processo e quello del SO è separato, questo per questioni di sicurezza**.

Inoltre ricordiamo che non è necessario eseguire un process switch ma soltanto un mode switch
### Kernel Basato sui Processi

^338496

> [!caption|right]
>
>![[2010241446.png]]

Qui **tutto è un processo** anche gli interrupt del Sistema Operativo, l’unica cosa che non lo è sono le funzioni che permettono il **process switching**. In questo caso quindi anche i processi del sistema operativo si trovano all’interno delle varie code.

---








