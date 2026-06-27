---
type: Uni Note
class:
  - "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2026-06-26T17:29
updated: 2026-06-27T16:12
---
## Introduzione

A differenza di altri sistemi operativi, UNIX adotta un approccio in cui quasi tutto viene trattato come un file. Esistono **6 tipi principali di file**:

- **Normale (Regular File):** Contiene dati generici (testo, eseguibili, immagini, ecc.). Il sistema operativo lo vede come una sequenza di byte.
- **Directory:** Un file speciale che contiene un elenco di nomi di file e i relativi puntatori ai rispettivi Inode. Permette la struttura gerarchica del File System.
- **Speciale (Device File):** Mappa i dispositivi di I/O hardware (dischi, terminali, schede di rete) come se fossero file, consentendo di comunicare con loro tramite le normali API di lettura/scrittura.
- **Named Pipe (FIFO):** Un file utilizzato per la comunicazione interprocesso (IPC), che permette a due processi indipendenti di scambiarsi dati.
- **Hard Link:** Un nome alternativo (un alias) per un file esistente. Più Hard Link puntano esattamente allo stesso Inode.
- **Link Simbolico (Symlink):** Un file scorciatoia che contiene semplicemente il percorso testuale (il nome) del file a cui si riferisce.

## L'Inode (Index Node)

L'**Inode** è la struttura dati fondamentale del File System UNIX. Contiene tutti i metadati e le informazioni essenziali per descrivere un file, ad eccezione del suo nome (che è memorizzato nella directory).

- **Allocazione:** Di norma, esiste un Inode univoco per ogni file. Tuttavia, tramite gli _Hard Link_, più nomi di file possono riferirsi allo stesso Inode.
- **Posizione:** Tutti gli inode risiedono stabilmente sul disco. Quelli associati ai file attualmente aperti vengono caricati e mantenuti in RAM.
- **Identificazione:** Ogni file è identificato univocamente dal sistema tramite un **numero di Inode** (Index Number).

>[!note] Informazioni contenute nell'Inode
>
>- Identificatori dell'utente proprietario (UID) e del gruppo (GID).
>- Permessi di accesso (Read, Write, Execute per Owner, Group, Others).
>- Timestamp temporali: data di creazione, ultimo accesso (lettura) e ultima modifica (scrittura).
>- Flag di stato del sistema (utente e kernel).
>- Dimensione totale del file in byte.
>- Numero di blocchi fisici allocati, dimensione dei blocchi e puntatori ai blocchi di dati.
>- Se l'inode si riferisce a una directory, il numero di file/collegamenti in essa contenuti.

>[!warning] Dimensione Effettiva vs. Dimensione su Disco
>
>Quando si analizzano le proprietà di un file, si notano due valori distinti:
>
>1. **Dimensione del file:** La dimensione reale dei dati utili contenuti (es. un file di testo con 100 caratteri occupa 100 byte). 
>2. **Dimensione su disco:** Lo spazio fisico effettivamente occupato sul supporto di memoria. Il File System alloca lo spazio tramite **blocchi di dimensione fissa** (es. 4 KB).
 >
>> ⚠️ ***Nota sull'allocazione:***  Se un file è lungo solo 100 byte, sul disco occuperà comunque un intero blocco da 4096 byte. Lo spazio rimanente non utilizzato nel blocco viene sprecato (*frammentazione interna*). Per questo motivo, la dimensione su disco è quasi sempre superiore o uguale a quella effettiva.

## Allocazione dei Blocchi e Puntatori Multi-livello

Per gestire file di qualsiasi dimensione (da pochi byte a molti gigabyte) senza sprecare spazio nell'Inode, UNIX utilizza una struttura di **allocazione indicizzata multi-livello**.

### La Struttura dei Puntatori

L'Inode contiene un array fisso di puntatori (solitamente 13 o 15). Se prendiamo come esempio lo standard classico con 13 puntatori totali, la struttura funziona così:

1. **Puntatori Diretti (Direct Pointers):** I primi puntatori (es. i primi 10) puntano direttamente ai blocchi sul disco contenenti i dati veri e propri del file. Ideale per i file piccoli, poiché l'accesso ai dati è immediato. La capacità massima coperta dai puntatori diretti è pari a:

$$\text{Dimensione Massima Diretta} = \text{Numero Puntatori Diretti} \times \text{Dimensione Blocco}$$

2. **Puntatore Indiretto Singolo (Single Indirect):** Se il file cresce, il puntatore successivo non punta ai dati, ma a un **blocco di puntatori** intermedi. Ognuno di questi puntatori intermedi punta poi a un blocco di dati.

3. **Puntatore Indiretto Doppio (Double Indirect):** Punta a un blocco di puntatori, dove ogni elemento punta a un ulteriore blocco di puntatori, i quali infine puntano ai blocchi di dati.

4. **Puntatore Indiretto Triplo (Triple Indirect):** Aggiunge un terzo livello di indirection per supportare file di dimensioni enormi.

![[Pasted image 20260626175153.png|700]]


>[!note] Vantaggio dell'Agnosticismo dei Blocchi
>
>I blocchi sul disco non hanno bisogno di un contrassegno logico per indicare se contengono dati o puntatori. Il sistema operativo sa esattamente come interpretarli partendo dall'Inode, poiché conosce il livello di profondità del puntatore che sta seguendo.

### Esempio Pratico di Calcolo della Capacità

Ipotizziamo un sistema con blocchi da **4 KB** ($4096 \text{ Byte}$) e puntatori ad indirizzi a **4 byte**:

Il numero di puntatori che possono essere memorizzati in un singolo blocco intermedio è:

$$N = \frac{4096 \text{ Byte}}{4 \text{ Byte}} = 1024 \text{ puntatori}$$
Grazie a questo fattore di moltiplicazione, la capacità di memorizzazione cresce esponenzialmente ad ogni livello:
- **Livello Singolo:** Può indirizzare fino a $1024$ blocchi di dati
	- $\text{Spazio totale} = 1024 \times 4 \text{ KB} = 4 \text{ MB}$
- **Livello Doppio:** Può indirizzare fino a $1024 \times 1024 = 1024^2$ blocchi di dati
	- $\text{Spazio totale} = 1024^2 \times 4 \text{ KB} = 4 \text{ GB}$
- **Livello Triplo:** Può indirizzare fino a $1024 \times 1024 \times 1024 = 1024^3$ blocchi di dati.
	- $\text{Spazio totale} = 1024^3 \times 4 \text{ KB} = 4 \text{ TB}$

## Inode e Directory

Nel mondo UNIX, una **directory** non è altro che un file speciale. Al suo interno non contiene i dati dei file, ma una tabella composta da coppie chiave-valore:

$$\text{(Nome del File, Puntatore al relativo numero di Inode)}$$

Poiché una directory può contenere al suo interno altre coppie che puntano a loro volta a directory successive, si viene a creare la classica **struttura gerarchica ad albero** del File System.

## Accesso ai File e Gestione dei Permessi

Per poter compiere un'operazione su un file (es. leggerlo o modificarlo), il sistema operativo deve verificare che l'utente sia abilitato a farlo. In UNIX, la sicurezza è gestita tramite una **terna di permessi** applicata a **tre categorie di utenti**.

>[!note] Le 3 Categorie di Permessi
>- **Lettura (r - Read):** Permette di visualizzare il contenuto del file (o l'elenco dei file se si tratta di una directory).
>- **Scrittura (w - Write):** Permette di modificare o eliminare il file (o aggiungere/rimuovere file in una directory).
>- **Esecuzione (x - Execute):** Permette di eseguire il file come un programma o un comando (o di "entrare" in una directory con il comando `cd`).

>[!note] Le Tre Categorie di Utenti
>
>Le autorizzazioni vengono assegnate a:
>
>1. **Proprietario (User / Owner):** L'utente che ha creato il file (o a cui è stato assegnato).
>2. **Gruppo (Group):** Un insieme di utenti che condividono gli stessi privilegi su quel file.
>3. **Altri (Others):** Qualsiasi altro utente del sistema che non sia il proprietario e non faccia parte del gruppo.
## Gestione dei File Condivisi (Link)

Quando più utenti o applicazioni hanno bisogno di accedere allo stesso identico file posizionato in directory diverse, duplicare il file sarebbe inefficiente (spreco di spazio e problemi di sincronizzazione delle modifiche). UNIX risolve questo problema con due meccanismi:

>[!note] Collegamenti Simbolici (Symbolic Links / Symlinks)
>
>Un link simbolico è un vero e proprio file indipendente che contiene semplicemente una stringa di testo: il **percorso (cammino) assoluto o relativo** verso il file originale.
>
>- **Funzionamento:** Quando il sistema apre il symlink, legge il percorso contenuto e viene reindirizzato al file di destinazione.
>- **Caratteristica chiave:** Se il file originale viene eliminato o spostato, il link simbolico rimane intatto ma diventa **orfano** (dangling link), puntando a un percorso non più esistente.

>[!note] Collegamenti Fisici (Hard Links)
>
>Un hard link è un nome alternativo (un alias) che punta **direttamente allo stesso numero di Inode** del file originale.
>
>- **Funzionamento:** Non esiste una distinzione reale tra il "primo" file e l'hard link: sono due nomi diversi che puntano alla stessa identica struttura dati sul disco.
>
>- **Gestione della cancellazione:** L'Inode contiene un **contatore dei collegamenti** (link count). Ogni volta che si crea un hard link, il contatore sale di 1, quando un file viene eliminato (`rm`), il contatore scende di 1. 
>  
>Il file e i suoi dati sul disco vengono effettivamente cancellati **solo quando il contatore dei link raggiunge lo zero**, ovvero quando viene rimosso l'ultimo nome associato a quell'inode.
