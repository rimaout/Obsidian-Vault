---
type: Uni Note
class:
  - "[[Sistemi Operativi 2 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-10-03T19:10
updated: 2025-10-05T16:04
---
## File System

Il file system un area di memoria organizzata in file e directory, sia le directory che i file sono rappresentati da un struttura dati chiamata I-Node:
- Le directory sono i node contente una lista di file/directory
- Le directory formano una struttura ad albero gerarchica

## Struttura inode

Ogni file nel filesystem è rappresentato da una struttura dati *inode* ed è univocamente identificato da un **inode number**. La **cancellazione** di un file *libera l’inode number* che verra’ riutilizzato quando necessario per un nuovo file.

Principali attributi struttura dati *inode*:
- ***Type:*** Tipo di file (regular, block, fifo ...)
- ***User ID:*** Id dell'utente proprietario del file
- ***Group ID:*** Id del gruppo a cui e associato il file
- ***Mode:*** [[Permessi File Linux|Permessi]] (read, write, exec) di accesso per il proprietario, il gruppo e tutti gli altri
- ***Size:*** Dimensione in byte del file
- ***Timestamps:*** `ctime` (inode changing time), `mtime` (content modication time), `atime` (content access time)
- ***Link count:*** Numero di hard links
- ***Data pointers:*** Puntatore alla lista dei blocchi che compongono il file; se si tratta di una directory, il contenuto su disco e costituito di una tabella con 2 colonne: nome del file/directory e suo inode number.
## Visualizzare informazioni

>[!note] Comando "ls"
>Per visualizzare le informazioni di un *inode* possiamo utilizzare il comando `ls nomedir/nomefile`, a cui possono essere concatenate queste flag opzionali: `[-a] [-c] [-u] [-R] [-l] [-i] [-n] [-S] [-h] [-1]`:
>- `-i`: mostra l'*inode number*
>- `-l`: mostra *diritti*, *num_of_dirs*, *user*, *group*, *date*, *size*, *time* e la dimensione in blocchi dello spazzino occupato dalla directory, `num_of_dirs` rappresenta il numero di directory contenute della directory su cui abbiamo effettuato `ls` (vengono contante anche . e .. ) (se ls chiamato su un file ritorna `1`)
>- `-n`: mostra le stesse informazioni di `-l` ma consente di visualizzare ID utente e ID gruppo invece del nome esteso
>- `ls -lc nomefile` per mostarre *ctime*
>- `ls -lu nomefile` per mostarre *atime*
>- `ls -l nomefile` (senza niente) per mostrare *mtime*
>- `ls -r` mostra il contenuto della directory ma reversed
>- `ls -R` mostra il contenuto della directory e di tutte le directory figlie (recursive)