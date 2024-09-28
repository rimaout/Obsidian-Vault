---
type: Uni Note
class: 
academic year: 2023/2024
related: 
completed: false
created: 2024-09-27T17:20
updated: 2024-09-28T11:17
---
>[!abstract] Index
>1. [[#Introduzione]]
>2. [[#Interruzioni Sincrone ed Asincrone]]
>3. [[#Approfondimento Causa Interruzioni]]
>4. [[#Termine di un Interruzione]]

>[!abstract] Related
>- [[Sistemi Operativi 1 (class)]]

---
## Introduzione

Le **Interruzioni** sono un meccanismo fondamentale di un qualsiasi sistema operativo che permette di interrompere il processo in esecuzione sul processore.

Le cause per cui potrebbe avvenire un interruzione sono molteplici, e danno luogo a diversi tipi di interruzioni:
- da programma (**sincrone**)
- da I/O (**asincrone**)
- da fallimento hardware (**asincrone**)
- da timer (**asincrone**)

---
## Interruzioni Sincrone ed Asincrone

>[!note] Sincrone
>Interruzioni che si verificano in come **immediata** conseguenza dell'esecuzione una un istruzione che richiede l'intervento del sistema operativo.
>
>Le interruzioni sincrone (al contrario di quelle asincrone) non vengo sollevate da eventi esterni, ma soltanto dal "codice" in esecuzione nel Thread, per questo vengono anche chiamate **interruzioni da programma**.
>
>Esempi di interruzioni da programma sono:
>- Una chiamata di sistema ([[System Call]]) per accedere a delle risorse di sistema (esempio lettura/scrittura di un file)
>- Errori come come richiesta di accesso a memoria protetta o non presente.

>[!note] Asincrone
>Interruzioni che vengono tipicamente sollevate (molto) dopo l’istruzione che le ha causate, alcune interruzioni asincrone sono sollevate non da istruzioni eseguite nei thread ma da eventi esterni come:
>- Interruzioni da input/output
>- Interruzioni da fallimento HW
>- Interruzioni da comunicazione tra CPU (per multi processor systems)
>- Interruzioni da timer (usati per eseguire più processi)

## Approfondimento Causa Interruzioni

>[!note] Input/Output
> La maggior parte dei dispositivi di input o output sono più lenti del processore, quindi, il processore manda un comando al dispositivo di I/O e poi aspetta che il dispositivo lo “interrompa” quando è riuscito a completare la richiesta segnalano il completamento o l’errore di un’operazione di I/O.

>[!note] Fallimento Hardware
>Interruzione che si verifica quando un dispositivo hardware del sistema non funziona correttamente o si verifica un errore hardware.

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

>[!note] Programma
>Interruzione causate dall’esecuzione di un istruzione del programma in psucuzione che richiede l'intervento del sistema operativo.
>
>**Cause principali sono:**
>- overflow
>- divisione per 0
>- debugging: single step o breakpoint
>- riferimento ad indirizzo di memoria fuori dallo spazio disponibile al programma
>- riferimento ad indirizzo di memoria momentaneamente non disponibile
>- memoria virtuale: 
>- Istruzione macchina errata (opcode illegale, oppure operando non allineato)
>- chiamata a system call (intenzionale)
>
>>**oss:** Vengono anche chiamate **exception** nei processori intel.

---
## Termine di un Interruzione

>[!note] Interruzione Asincrona
Al termine di un interruzione **asincrona** si riprende dall’istruzione subito successiva a quella dove si è verificata l’interruzione.
>
>>**oss:** Solo se la computazione non è stata completamente abortita come conseguenza dell’interruzione.

>[!note] Interruzione Sincrona
Al termine di un interruzione **sincrona** ci sono tre possibili casistiche:
>1. **Faults:** errore correggibile, viene rieseguita la stessa istruzione dove è avvenuta l’interruzione.
>2. **Aborts:** errore non correggibile, si esegue software collegato con l’errore.
>3. **traps e system calls:** si continua dall’istruzione successiva.

