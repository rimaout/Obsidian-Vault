---
type: Uni Note
class:
  - "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2024-10-01T16:00
updated: 2026-01-31T13:32
---

>[!abstract] Related
>- [[Sistemi Operativi 1 (class)]]

---
## Cos'è?

Il Sistema Operativo è un programma che gestisce il funzionamento di altri programmi, prepara i loro ambienti, li manda in esecuzione, gestisce errori. È fa da **interfaccia** tra hardware e software.

Infatti è un normale programma in esecuzione con il suo ciclo di _fetch / execute_ ma ha privilegi più alti, in alcuni casi può passare questi privilegi ad altri programmi.

>[!note] Servizi di un sistema operativo
>
>Le funzionalità di base per l'utente offerte dai sistemi operativi moderni sono:
>- **Esecuzione di programmi** anche in contemporanea.
>- Accesso ai **dispositivi I/O**.
>- Accesso al Sistema Operativo stesso tramite **shell**.
>- **Sviluppo di Programmi** quindi compilatori, syscalls, debugger ecc…
>- Rilevamento e reazione ad errori hardware / software.
>- **Accounting** ovvero una collezione di statistiche di sistema e monitoraggio delle risorse. Viene utilizzato per capire cosa migliorare.

---
## Kernel 

Il kernel è il livello più basso del sistema operativo e si trova tra l'hardware e gli altri componenti del sistema operativo. 

È responsabile di fornire un'interfaccia standard per l'accesso alle risorse hardware, in modo che gli altri componenti del sistema operativo possano utilizzarle in modo trasparente.

>[!tip] Nota
>- È  sempre presente nella memoria principale (RAM)
>- La traduzione letterale è **nucleo**

---
## Programmazione Singola e Multi Programmazione

>[!note] Programmazione Singola
>La programmazione singola è un approccio in cui un solo processo o programma viene eseguito alla volta. Il sistema operativo esegue un processo fino al suo completamento prima di passare al successivo. 
>
>>**Svantaggio Principale:** quando un processo è in attesa di un input il processore rimarrà inutilizzato.
>
>![[Pasted image 20241001164941.png|650]]

>[!note] Multiprogrammazione
>La multi programmazione è una tecnica che si basa sul idea che un processore deve poter eseguire più programmi contemporaneamente, condividendo le risorse del sistema.
>
>![[Pasted image 20241001165009.png|600]]

^56705c

>[!warning] Esempio processo I/O bound
>![[Pasted image 20241001164822.png|300]]

---
## Batch e Time Sharing

I casi visti precedentemente ([[#Programmazione Singola e Multi Programmazione|qui]]) sono basiti su sistemi **Batch**

>[!note] Batch
>Un **Sistema Batch** che eseguono programmi in modo sequenziale, senza intervento umano diretto. I sistemi Batch sono considerati statici ovvero, le istruzioni da eseguire sono definite in anticipo e non cambiano durante l'esecuzione.
>
>>**Svantaggi:** Non adatti a sistemi con iterazione utente, e multi user.

>[!note] Time Sharing
> Un sistema **Time Sharing** è sistema operativo che consente a più utenti di accedere e utilizzare le risorse di un computer contemporaneamente, permettendo
> - L'esecuzione processi in "parallelo".
> - L'esecuzione di processi interattivi.
> - La condivisione delle risorse hardware.
>
>Questo è permesso grazie allo **Scheduling**, ovvero un algoritmo che decide quale utente e processo deve essere eseguito in ogni **time slice**.
>
>I **Time Slice**: il sistema divide il tempo di esecuzione della CPU in piccoli intervalli di tempo, chiamati "time slice" o "quantum". Ogni utente e processo ha a disposizione un certo numero di time slice per eseguire le proprie istruzioni.
>
>>[!warning] Multi Programmazione
>>Il time sharing permette la multi programmazione, infatti appena un processo deve eseguire un'operazione di I/O (Input/Output), come ad esempio leggere da un file o stampare su una stampante, il sistema operativo può sospendere il processo e assegnare la CPU ad un altro processo che è pronto per essere eseguito.
 
|                                     | **Batch**                                                       | **Time Sharing**                  |
| ----------------------------------- | --------------------------------------------------------------- | --------------------------------- |
| **Scopo principale:**               | Massimizzare l’uso del processore.                              | Minimizzare il tempo di risposta. |
| **Provenienza Direttive per l'OS:** | Comandi del job control language, sottomessi con il job stesso. | Comandi dati da terminale         |

## Struttura del Sistema Operativo

Un sistema operativo è un software enorme, per questo le sue funzionalità sono state divise in livelli.

![[Pasted image 20250821175846.png|500]]

Ogni livello si basa su quello più sotto:
- Livello 1:
    - Circuiti elettrici
    - Registri, celle di memoria, porte logiche
    - Operazioni come reset di un registro o leggere in una locazione di memoria
- Livello 2:
    - Insieme delle istruzioni macchina come _add, sub, load, store_.
- Livello 3:
    - Aggiunge il concetto di routine, operazioni di chiamata e ritorno.
- Livello 4:
    - Interruzioni.
- Livello 5:
    - Processo come programma in esecuzione.
    - Sospensione e ripresa di un processo.
- Livello 6:
    - Dispositivi di memorizzazione secondaria
    - Trasferimento di blocchi di dati
- Livello 7:
    - Crea uno spazio logico degli indirizzi per i processi.
    - Organizza lo spazio degli indirizzi virtuali in blocchi
- Livello 8:
    - Comunicazioni fra processi
- Livello 9:
    - Salvataggio di file a lungo termine
- Livello 10:
    - Accesso a dispositivi esterni con interfacce standard
- Livello 11:
    - Associazione tra identificatori interni ed esterni
- Livello 12:
    - Supporto di alto livello per i processi
- Livello 13:
    - Interfaccia utente

## Kernel Moderno di Linux

I moderni kernel sono *monolitici* o *microkernel*:

- **Monolitico** - Tutto il sistema operativo viene caricato in RAM all’accensione.
- **Microkernel** - Solo una minima parte del S.O. viene caricato in RAM e il resto solo quando serve.
    - Sempre in memoria: scheduler, sincronizazzione.
    - Solo a richiesta: gestore memoria, filesystem, driver.

Il monolitico è più efficiente in velocità ma ovviamente occupa più memoria RAM.

>[!note] Nel mondo reale
>
>Quasi tutti i sistemi moderni sono a kernel monolitico ad eccezione di MacOS.
>
>Linux invece è principalmente monolitico ma ha dei moduli:
>
>- Alcune parti del sistema operativo possono essere caricate solo quando servono, la differenza è che in Linux cosa serve e cosa no lo decide l’utente e non il sistema operativo.
>- Le cose che Linux non carica sono vari filesystem che non gestisce, driver per alcuni dispositivi, funzionalità di rete.
