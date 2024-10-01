---
type: Uni Note
class:
  - "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related: 
completed: true
created: 2024-10-01T16:00
updated: 2024-10-01T19:12
---
>[!abstract] Index
>1. 

>[!abstract] Related
>- 

---
## Cos'è?

Il sistema operativo è un software fondamentale che:
- Gestisce le risorse hardware di un computer, e premette l'interazione con l'utente.
- Gestione dei programmi applicativi, gli prepara l’ambiente, li manda in esecuzione, risponde a loro eventuali richieste, gestisce la loro terminazione
- Interfaccia tra le applicazioni e l’hardware

>[!warning] Obiettivi di un sistema operativo
>- Convenienza
>- Efficienza
>- Capacità di evolvere

---
## Servizi di un sistema operativo

Le funzionalità di base per l'utente offerte dai sistemi operativi moderni sono:

>[!warning] Esecuzioni di programmi
>- app (ovvero software avviato dall'utente)
>- sevizi (ovvero software avviato all'avvio del sistema)
>- la possibilità di eseguire più servizi e applicazioni contemporaneamente

>[!warning] Accesso a dispositivi di input/output
>- principalmente interfaccia con le memorie grazie al FileSystem

>[!warning] Accesso al OS
>- Attraverso shell

>[!warning] Sviluppo di programmi
>- compilatore, editor e dubuger
>- system calls
>- visione semplificata  della RAM

>[!warning] Gestione di errori 
>- Rilevamento di errori e gestione delle conseguenze.
>- tippi:
>	- errori hardware interno o esterno
>	- errori software
>	- richieste di un dispositivo non soddisfacibili

>[!warning] Accounting
>- collezione di statistiche dell’uso del sistema
>- monitoraggio delle performance
>- usato per capire cosa occorre migliorare
>- usato per far pagare in base all’uso del sistema

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
>![[Pasted image 20241001164941.png|400]]

>[!note] Multiprogrammazione
>La multi programmazione è una tecnica che si basa sul idea che un processore deve poter eseguire più programmi contemporaneamente, condividendo le risorse del sistema.
>
>![[Pasted image 20241001165009.png|400]]

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

---