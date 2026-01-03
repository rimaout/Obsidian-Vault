---
type: Uni Note
class:
  - "[[Sistemi Operativi 2 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-10-05T19:14
updated: 2025-10-07T08:56
---
## Rappresentazione dei processi

>[!note] PID - Process Identifier
>
>È un identificatore univoco di un processo quindi in un dato istante, non ci possono essere 2 processi con lo stesso PID.
>
>Una volta che un processo e’ terminato, il suo PID viene liberato, e potrebbe essere prima o poi riusato per un altro processo.

>[!note] Process Control Block
>
>- *PID:* Process Identifier
>- *PPID:* Parent Process Identifier
>- *Real UID:* Real User Identifier
>- *Real GID:* Real Group ID
>- *Effective UID:* Effective User Identifier (UID assunto dal processo in esecuzione)
>- *Effective GID:* Effective Group ID (come sopra per GID)
>- *Saved UID:* Saved User Identifier (UID avuto prima dell’eseccuzione del SetUID)
>- *Saved GID:* Saved Group Identifier (come supra per GID)
>- *Current Working Directory:* directory di lavoro corrente
>- *Umask:* file mode creation mask
>- *Nice:* priorita statica del processo
>  
>>[!warning] Differenza tra RUID e EUID
>>
>>Quando utilizziamo `SetUID` di un file eseguibile:
>>- `RUID` l’id di chi lo esegue
>>- `EUID` l’id del proprietario del file

>[!note] Aree di memoria
>- *Text Segment:* le istruzioni da eseguire (in linguaggio macchina)
>- *Data Segment:* i dati statici (ovvero, variabili globali e variabili locali static) inizializzati e alcune costanti di ambiente
>- *BSS:* I dati statici non inizializzati (sta per block started from symbol); la distinzione dal segmento dati si fa per motivi di realizzazione hardware
>- *Heap:* I dati dinamici (allocati con malloc e simili)
>- *Stack:* le chiamate a funzioni, con i corrispondenti dati dinamici (variabili locali non static)
>- *Memory Mapping Segment:* tutto cio che riguarda librerie esterne dinamiche usate dal processo, nonche estensione dello heap in alcuni casi

## Stato di un processo e modalità di esecuzione

^88b0db

**Stati di un processo:** ^dc2ba3
- *Running (R):* in esecuzione su un processore
- *Runnable (R):* pronto per essere eseguito (non e in attesa di alcun evento); in attesa che lo scheduler lo (ri)seleziona per l’esecuzione
- *(Interruptible) Sleep (S):* e in attesa di un qualche evento (ad esempio, lettura di blocchi dal disco), e non può quindi essere scelto dallo scheduler
- *Zombie (Z):* il processo e’ terminato e le sue 6 aree di memoria non sono più in memoria; tuttavia, il suo PCB viene ancora mantenuto dal kernel perché il processo padre non ha ancora richiesto il suo “exit status" (ritorneremo su questo punto)
- *Stopped (T):* caso particolare di sleeping: avendo ricevuto un segnale STOP, e in attesa di un segnale CONT
- *Traced (t):* in esecuzione di debug, oppure in generale in attesa di un segnale (altro caso particolare di sleeping; vedremo più avanti)
- *Uninterruptible sleep (D):* come sleep, ma tipicamente sta facendo operazioni di IO su dischi lenti e non puo essere interrotto ne ucciso

>[!note] Esecuzione Foreground
>- Il comando puo leggere l'input da tastiera e scrivere su schermo
>- Finche non termina, il prompt non viene restituito e non si possono sottomettere altri comandi (o job...) alla shell

>[!note] Esecuzione Background
>
>Il comando non può leggere l'input da tastiera ma può scrivere su schermo.
>- il prompt viene immediatamente restituito;
>- mentre il job viene eseguito in background, si possono da subito dare altri comandi alla shell

