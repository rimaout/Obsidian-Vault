---
type: Uni Note
class:
  - "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2026-06-25T15:30
updated: 2026-06-25T18:54
---
## FIle

I file sono l'elemento principale per la maggior parte delle applicazioni, questo perché molto spesso, l’*input* di un’applicazione è un file, e quasi altrettanto spesso l’*output* è un file.

I file hanno le seguenti obbiettivi:
- Esistenza a lungo termine dei file (“sopravvivono” ad un processo terminato)
- Diversi processi utilizzano gli stessi file (tramite nome simbolici)
- Strutturabilità (directory gerarchiche), ovvero un sistema di organizzazione per aiutare l’utente a trovare i file

## File System

I file sono gestiti da un insieme di programmi e librerie, eseguiti in **kernel mode**, che insieme formano il *File (Management) System*.

Lavorano con la memoria secondaria (dischi, chiavi USB, ...) ma in Linux, anche in RAM.

>[!note] Operazioni Fronite
>
>- Mantenimento dei **metadati** per ogni file (proprietario, data di creazione, etc)
>- **Creazione** (con annessa scelta del nome), il file appena creato è vuoto.
>- **Cancellazione**
>- **Apertura**: necessaria per poter leggere e scrivere
>- **Lettura**: solo su file aperti
>- **Scrittura**: solo su file aperti
>- **Chiusura**: necessaria per le performance

## Campi e Record

La memorizzazione logica dei dati segue una precisa gerarchia, dal dato elementare alla struttura complessa:

$$\text{Byte} \rightarrow \text{Campo} \rightarrow \text{Record} \rightarrow \text{File} \rightarrow \text{Database}$$

- **Campi:** Sono i dati di base. Contengono valori singoli caratterizzati da una precisa lunghezza e da un tipo di dato (es. un carattere ASCII, un numero intero).
- **Record:** Sono insiemi di campi correlati tra loro e trattati dall'applicazione come un'unica unità logica.
	- _Esempio:_ Il record "Impiegato" è composto dai campi _Nome_, _Cognome_, _Matricola_ e _Stipendio_.

## File e Database

- **File:** Raccolte di record dello stesso tipo dotate di un nome proprio. Implementano meccanismi di **controllo degli accessi** (permessi utente per decidere chi può leggere, scrivere o modificare il file).
- **Database:** Collezioni di dati e file correlati. A differenza dei singoli file, i database non si limitano a memorizzare i dati, ma **mantengono ed esplicitano le relazioni** tra di essi. Sono gestiti dai **DBMS (Database Management System)**, che si eseguono come processi del Sistema Operativo.

> [!warning] Cambio di paradigma nei Sistemi Operativi Moderni
> 
> Storicamente (es. nei vecchi Mainframe), il Sistema Operativo conosceva la struttura interna dei file (campi e record) e aiutava i programmi a leggerli riga per riga.
> 
> Nei **SO generici moderni** questo approccio è stato rimosso: il SO è **agnostico** (non gli interessa il contenuto). Per il File System, un file è semplicemente una **sequenza lineare di byte** (da qui la frase _"ogni record è un solo campo con un byte"_).
> 
> Sta interamente a chi progetta l'applicazione decidere come interpretare quel flusso di byte (es. Excel interpreterà le virgole di un file `.csv` per ricostruire la griglia di campi e record).

## File Management System (FMS)

**File Management System (FMS)** è la parte di SO che solleva i programmatori dal dover scrivere codice di basso livello per interagire con l'hardware dei dischi, fornendo servizi utente per l'utilizzo di file.

>[!note] Obiettivi di un FMS
>
>1. **Soddisfare le necessità dell'utente** relative alla gestione e archiviazione dei dati.
>2. **Garantire l'integrità dei dati**, evitando che si corrompano.
>3. **Ottimizzare le prestazioni** complessive del sistema di storage.
>4. **Fornire supporto nativo per diversi supporti** di memoria secondaria (HDD, SSD, USB, CD/DVD).
>5. **Minimizzare il rischio di perdita** o distruzione dei dati (gestione dei guasti).
>6. **Fornire API/Interfacce standard** per i processi utente.
>7. **Gestire l'I/O concorrente**, permettendo l'accesso simultaneo a più utenti.

>[!note] Requisiti di un FSM (Cosa deve poter fare l'utente):
>
>- Creare, cancellare, leggere e modificare i file.
>- Accedere in modo controllato e protetto ai file di altri utenti (se autorizzato).
>- Controllare, leggere e modificare i permessi di accesso dei propri file.
>- Ristrutturare i propri file in modo attinente al problema (strutturazione logica a livello applicativo).
>- Spostare o copiare dati da un file all'altro.
>- Mantenere e gestire copie di backup per il disaster recovery.
>- Accedere ai file tramite nomi simbolici mnemonici scelti dall'utente (es. `appunti.txt`) anziché tramite indirizzi fisici.
  
>[!note] Suddivisione del Lavoro
>
>![[Pasted image 20260625185052.png|110]]
>
>- **Directory Management**: Sono tutte le operazioni utente che hanno a che fare con i file come crearli, cancellarli ecc… In questa fase si passa da nomi di file a identificatori.
>- **File System**: Struttura logica delle operazioni (apri, chiudi, leggi, scrivi …)
>- **Organizzazione fisica**: Dagli identificatori dei file si passa agli indirizzi fisici sul disco. Decide dove mettere i file e come posizionarli.
>- **Scheduling & Control**: Qui avvengono i vari SCAN ([[Scheduling del disco (HDD) - SO1|Scheduling dell'disco]])