---
type: Uni Note
class:
  - "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2024-09-27T17:20
updated: 2025-08-22T12:26
---
>[!abstract] Related
>- [[Sistemi Operativi 1 (class)]]

---
## Introduzione

Le **Interruzioni** sono un meccanismo fondamentale di un qualsiasi sistema operativo che permette di interrompere il processo in esecuzione sul processore.

Le cause per cui potrebbe avvenire un interruzione sono molteplici, e danno luogo a diversi tipi di interruzioni:
- da programma ([[#^8c821c|sincrone]])
- da I/O ([[#^e40f58|asincrone]])
- da fallimento hardware ([[#^e40f58|asincrone]])
- da timer ([[#^e40f58|asincrone]])

---
## Interruzioni Sincrone ed Asincrone

>[!note] Sincrone
>Interruzioni che si verificano come **immediata** conseguenza dell'esecuzione un'istruzione che richiede l'intervento del sistema operativo.
>
>Le interruzioni sincrone (al contrario di quelle asincrone) non vengo sollevate da eventi esterni, ma soltanto dal "codice" in esecuzione nel Thread, per questo vengono anche chiamate **interruzioni da programma**.
>
>Esempi di interruzioni da programma sono:
>- Una ***chiamata di sistema*** (System Call) per accedere a delle risorse di sistema (esempio lettura/scrittura di un file)
>- Degli ***errori***, come una richiesta di accesso a memoria protetta o non presente.

^8c821c

>[!note] Asincrone
>Interruzioni che vengono tipicamente sollevate (molto) dopo l’istruzione che le ha causate, alcune interruzioni asincrone sono sollevate non da istruzioni eseguite nei thread ma da eventi esterni come:
>- Interruzioni da input/output
>- Interruzioni da fallimento Hardware
>- Interruzioni da comunicazione tra CPU (per multi processor systems)
>- Interruzioni da timer (usati per eseguire più processi)

^e40f58

---
## Approfondimento Causa Interruzioni

>[!note] Programma
>Interruzione causate dall’esecuzione di un istruzione (di un programma) che richiede l'intervento del sistema operativo.
>
>**Cause principali sono:**
>- ***Intenzionale:*** 
>	- chiamata a system call
>	- debugging: single step o breakpoint
>- ***Non intenzionale:***
>	- overflow
>	- divisione per 0
>	- riferimento ad indirizzo di memoria fuori dallo spazio disponibile al programma
>	- riferimento ad indirizzo di memoria momentaneamente non disponibile
>	- Istruzione macchina errata (opcode illegale, oppure operando non allineato) 
>
>>**oss:** Vengono anche chiamate **exception** nei processori intel.

>[!note] Input/Output
>La maggior parte dei dispositivi di input/output (I/O) sono più lenti del processore.
>
>Quando il processore ha bisogno di eseguire un'operazione di I/O, manda una richiesta al dispositivo di I/O e poi aspetta che il dispositivo lo informi quando l'operazione è completata. 
>
>Il dispositivo di I/O segnala il completamento o l'errore dell'operazione di I/O, invocando un interruzione sul processore.
>
>**Related:** [[Input Output - Introduzione]]

>[!note] Fallimento Hardware
>Interruzione che si verifica quando un dispositivo hardware del sistema non funziona correttamente.

>[!note] Comunicazione tra CPU
>Interruzione che si verifica quando una CPU richiede l'intervento di un'altra CPU in un sistema multiprocessore.

>[!note] Timer
>Interruzione che si verifica quando un timer hardware o software scade.
>
>Questi timers permettono al sistema operativo di eseguire alcune operazioni ad intervalli regolari, come:
>- Eseguire una routine di manutenzione del sistema
>- Aggiornare la data e l'ora del sistema
>- Eseguire una routine di backup dei dati
>- Gestire la pianificazione dei processi

---
## Termine di un Interruzione

>[!note] Interruzione Asincrona
>
>Al termine di un interruzione **asincrona** si riprende dall’istruzione subito successiva a quella dove si è verificata l’interruzione.
>
>>**nota:** Solo se la computazione non è stata completamente abortita come conseguenza dell’interruzione.

>[!note] Interruzione Sincrona
>
>Al termine di un interruzione **sincrona** ci sono tre possibili casistiche:
>1. **Faults:** errore correggibile, viene rieseguita la stessa istruzione dove è avvenuta l’interruzione.
>2. **Aborts:** errore non correggibile, si esegue software collegato con l’errore.
>3. **traps e system calls:** si continua dall’istruzione successiva.

---
## Fase di Interruzione 

Ad ogni **ciclo fetch-execute** dell'esecuzione di un istruzione, viene anche controllato se si è verificata un’interruzione (o exception)

Nel caso di un interruzione, il programma viene sospeso e viene eseguita una funzione che gestisce l’interruzione (**interrupt-handler routine**)

![[Pasted image 20240928115435.png|600]]

---
## Interruzioni Sequenziali ed Annidate

![[Pasted image 20240928120256.png|1000]]
