---
type: Uni Note
class:
  - "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related: 
completed: false
created: 2024-10-04T18:51
updated: 2024-10-05T16:35
---
>[!abstract] Index
>1. 

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
## Elementi

Finche un processo è in esecuzione, ad esso sono associate delle informazioni, tra le quali:
- Identificatore (per distinguerlo da altri processi)
- Stato (running... )
- Priorità 
- Hardware Context (valore corrente dei registi della CPU, compreso program counter)
- Puntatori a Memoria (immagine del processo)
- Stato dell'I/O
- Informazioni di accounting (utente che sta eseguendo il processo)

>[!note] Process Control Block
>
>>[!column|flex]
>>
>>>[!note|clean no-t]
>>>Insieme di informazioni create dal sistema operativo per ogni processo che:
>>>- Salvate nella zona riservata al [[Kernel]] (accessibile soltanto all'OS).
>>>- Contiene gli [[#Elementi]] del processo.
>>>- Permette la gestione di più processi, ovvero contiene sufficienti informazioni per bloccare un programma in esecuzione e farlo riprendere più tardi dallo stesso punto in cui si trovava.
>>
>>>[!caption|right]
>>> 
>>>![[Pasted image 20241004194346.png|120]]

---
## Stati

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

---
## Rappresentazione dell'esecuzione

![[Pasted image 20241005154848.png|450]]
![[Pasted image 20241005154908.png|450]]
![[Pasted image 20241005154929.png|450]]