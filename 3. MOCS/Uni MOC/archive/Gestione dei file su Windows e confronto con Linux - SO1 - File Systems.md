---
type: Uni Note
class:
  - "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2026-06-26T17:29
updated: 2026-07-01T11:21
---
## Introduzione

A differenza di UNIX, che standardizza tutto sul concetto di Inode, Windows è basato su due File System principali:
- **FAT (File Allocation Table):** Il ***vecchio*** file system di MS-DOS. Utilizza una tabella di puntatori concatenati. È limitato ma ampiamente compatibile, motivo per cui è ancora lo standard per le chiavette USB e i dispositivi portatili.
- **NTFS (New Technology File System):** Il file system ***moderno*** di Windows. Abbandona la vecchia tabella e gestisce lo spazio tramite una **bitmap** di blocchi a dimensione fissa chiamati **Cluster**, organizzando ogni file come un insieme di attributi all'interno di un indice master.

## FAT (File Allocation Table)

Il FAT (File Allocation Table) è un file system basato su una **tabella ordinata di puntatori**. Sebbene sia obsoleto per i dischi principali dei computer moderni, è ancora lo standard per le memorie flash (come le chiavette USB) grazie alla sua semplicità e compatibilità universale.
- **Versioni:** `FAT-12`, `FAT-16` e `FAT-32`. Il numero indica i bit utilizzati per ogni record della tabella.
- **Cluster:** L'unità base di memorizzazione, dimensionata tra `2 KB` e `32 KB` (scelta dall'utente durante la formattazione).
- **Problema di scalabilità:** Più il disco è grande e i cluster sono piccoli, più la tabella FAT diventa enorme.

>[!note] Struttura
>
>Il disco formattato in FAT viene diviso in quattro regioni principali.
>
>![[Pasted image 20260627235028.png|900]]
>
>
>| Regione        | Funzione e Caratteristiche                                                                                                                                                          |
>| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
>| **Boot Sector**    | Contiene il bootloader del sistema operativo, la tipologia del volume e i puntatori alle altre sezioni.                                                                                 |
>| **Regione FAT**    | È la "mappa" del disco. Contiene i record che indicano a quali file/directory appartengono i cluster. Ne esistono **due copie** per sicurezza (in caso di corruzione).                  |
>| **Root Directory** | Contiene le informazioni (file entry) della directory principale. In FAT12/16 ha un limite fisso di 256 voci. In FAT32 è spostata nella Regione Dati e non ha limiti.                   |
>| **Regione Dati**   | Contiene i dati effettivi dei file e le sottodirectory. Ogni entry di una directory occupa 32 byte e contiene: nome, attributi, timestamp e l'*indirizzo del primo cluster* del file. |

>[!note] Funzionamento (Lista Concatenata)
>
>Ogni directory entry (da `32 byte`) contiene i metadati del file (nome, attributi, timestamp) e il **puntatore al primo cluster**. Da lì, il file system interroga la tabella FAT riga per riga per ricostruire il file:
>
>- **Valore 0:** Il cluster è libero.
>- **Valore numerico (es. 5):** Indica che il file continua. Significa "vai al blocco 5 per leggere i prossimi dati, e guarda la riga 5 della FAT per scoprire dove andare dopo".
>- **Tutti 1 / Valore Speciale (es. FFFF):** End of File (EOF). Indica che ci troviamo nell'ultimo blocco del file.
>
>![[Pasted image 20260628150312.png]]
>
>![[Pasted image 20260628150443.png]]

>[!warning] Limitazioni
>
>- **Dimensione massima file:** `4GB`. Questo perché nella directory entry il campo che registra la grandezza del file è di soli `32 bit` (il valore massimo esprimibile è $2^{32}-1$ byte).
>- **Dimensione massima partizione:** `2TB` (usando settori standard da `512B`).
>- **Affidabilità:** Non implementa il _Journaling_, rendendolo vulnerabile alla corruzione in caso di spegnimenti improvvisi.
>- **Sicurezza:** Non supporta meccanismi di controllo degli accessi (ACL) o permessi per file e directory.

## NTFS (New Technology File System)

NTFS risolve i limiti strutturali di FAT introducendo:
- un'architettura più robusta:
- il supporto a nomi file in **UNICODE** (fino a 255 caratteri)
- il **Journaling** (per evitare la corruzione dei dati tracciando i metadati)
- il supporto per Hard e Soft links

### Struttura

In NTFS, **ogni file è un insieme di attributi** rappresentati come flussi di byte (_byte stream_). Perfino il contenuto stesso del file (i dati) è considerato semplicemente un attributo.

![[Pasted image 20260627235618.png|700]]

L'intera struttura si basa sulla **MFT (Master File Table)**, un indice unico per ogni volume strutturato come una sequenza di record di dimensione fissa (da **1 KB** a **4 KB**). **Ogni file sul disco possiede un record dedicato nella MFT.**

Ogni record contiene coppie `(Tipo Attributo, Valore)`:
- **Attributi Residenti:** Se il valore dell'attributo è molto piccolo (es. un file di testo di pochi byte), viene salvato **direttamente dentro il record della MFT**, garantendo un accesso istantaneo senza toccare altre zone del disco.
- **Attributi Non Residenti:** Se l'attributo è grande (come i dati di un file normale), il record conterrà soltanto un **puntatore** alle sequenze di blocchi esterni sul disco.

### I Record di Sistema (Metadati)

I primi 27 record della MFT sono strettamente riservati al funzionamento interno del File System. Tra i più importanti troviamo:

- **Record 0 (MFT stessa):** Descrive la MFT stessa e la posizione di tutti i file nel volume.
- **MFT Mirror:** Una copia di backup dei primi record cruciali dell'MFT.
- **LogFile:** Contiene i dati di _Journaling_ per il ripristino del sistema in caso di crash.
- **Volume:** Informazioni sul volume (ID, etichetta, versione).
- **Bitmap:** Una tabella di bit che tiene traccia di quali blocchi sul disco sono liberi o occupati.

### Strategia di Allocazione: I Blocchi Contigui (Extents)

A differenza di UNIX (che usa i puntatori multi-livello nell'Inode) o di FAT (che usa le liste concatenate), NTFS descrive la posizione dei file grandi tramite coppie di numeri che identificano **zone contigue (Extents o Runs)**:

$$\text{Run Data} = (\text{Blocco di Inizio}, \text{Numero di Blocchi Contigui})$$

Questa tecnica permette di descrivere file enormi usando pochissimo spazio nell'MFT, a patto che il file non sia frammentato. Al termine della sequenza di coppie, una entry vuota segnala la fine del file.

![[Pasted image 20260628110314.png]]

#### Calcolo dello Spazio di Descrizione (Contiguo vs Frammentato)

Ipotizziamo blocchi da **1 KB**, attributi memorizzati a 64 bit (**8 Byte**) e quindi ogni coppia occupa $2 \times 8 = 16 \text{ Byte}$.


>[!note] Caso 1: File da 20 GB Contiguo
>Il file è diviso in 20 grandi sequenze contigue (da 1 milione di blocchi ciascuna).
>
>Servono 20 coppie + 1 coppia vuota di terminazione = 21 coppie totali.
>    
>$$\text{Spazio occupato nell'MFT} = 21 \times 16 \text{ Byte} = 336 \text{ Byte}$$
>    
>_Un file enorme da 20 GB viene descritto in appena 336 byte grazie alla contiguità._

>[!note] Caso 2: File da 64 KB Frammentato
>
>Il file è piccolo, ma frammentato in 64 blocchi separati sul disco (64 sequenze da 1 blocco).
> 
>Servono 64 coppie + 1 coppia vuota di terminazione = 65 coppie totali.
> 
>$$\text{Spazio occupato nell'MFT} = 65 \times 16 \text{ Byte} = 1040 \text{ Byte}$$
>
>_Un file piccolissimo richiede il triplo dello spazio di descrizione rispetto al caso precedente a causa della frammentazione._
>
>>[!warning] Struttura ad Albero per File Giganti 
>>
>>Se un file molto grande o molto frammentato da non entrare nel record principale dell'MFT, NTFS adotta un approccio simile agli Inode di UNIX:
>>-  il record base diventa un puntatore che rimanda a $N$ record secondari esterni per contenere le restanti coppie di puntatori.
>>  
>>![[Pasted image 20260628110414.png]]
### Gestione delle Aree Vuote: I File Sparsi (Sparse Files)

NTFS ottimizza lo spazio sul disco quando un file presenta ampie zone vuote.

Se un'applicazione crea un file virtuale da **1 GB** scrivendo effettivamente dati solo per **100 MB**, NTFS non scrive i restanti 900 MB di zeri sul disco fisico.

L'MFT memorizza la dimensione logica totale (**1 GB**) per il Sistema Operativo, ma imposta semplicemente a `0` i bit di allocazione delle aree vuote nella sua lista interna. Di conseguenza, il file occuperà fisicamente solo **100 MB** sul supporto reale, evitando sprechi di spazio.

## Confronto con File System Unix

>[!note] Struttura File System Unix
>
>Il File System Unix è organizzato logicamente in diverse regioni specifiche, ognuna con un compito fondamentale per il funzionamento del sistema:
>- **Boot Block (Blocco di avvio):** È molto simile al blocco di boot dei sistemi FAT. Contiene le informazioni e i dati essenziali necessari per il _bootstrap_ (la procedura di avvio del sistema operativo).
>- **Superblock:** Custodisce i metadati fondamentali del file system. Tra le informazioni principali troviamo:
>    - La dimensione delle partizioni.
>    - La dimensione dei blocchi.
>    - Il puntatore alla lista dei blocchi liberi.
>- **Lista degli I-node (i-list):** Si tratta di una tabella numerata che contiene i descrittori dei file, chiamati appunto **i-node** (_index node_).
>    - A ogni file salvato nel sistema corrisponde un i-node univoco.
>    - Ogni i-node contiene i puntatori che rimandano ai blocchi fisici in cui sono memorizzati i dati del file all'interno della sezione dati del volume.
>
>![[Pasted image 20260630145624.png|600]]
>
>>[!danger] Ridondanza Superblock
>>
>>Per prevenire perdite di dati in caso di corruzione, il sistema crea **copie ridondanti** del Superblock e le salva in vari gruppi di blocchi sparsi nel file system.
>>
>>Tuttavia, la copia "master" (la prima) si trova sempre in una posizione fissa e predefinita per facilitare e velocizzare le operazioni di _recovery_.

>[!note] Gestione dei File Aperti nel Kernel Unix
>
>Per gestire in modo efficiente i file aperti e i relativi i-node, il kernel Unix si appoggia a due strutture di controllo separate:
>
>1. **Puntatore locale (per processo):** Quando un file è attualmente in uso da parte di un processo, il puntatore al suo descrittore viene salvato all'interno del **Process Control Block (PCB)** di quel processo specifico.
>2. **Tabella globale dei file aperti:** È una struttura dati centrale mantenuta dal sistema operativo, che contiene l'elenco di tutti i descrittori dei file attualmente aperti a livello globale nel sistema.
>   
>![[Pasted image 20260701112105.png|600]]

## Confronto con File System in Linux

Linux supporta nativamente la famiglia di file system **ext** (Extended File System). Le differenze principali tra le versioni sono:
- **ext2:** È l'implementazione base, derivata direttamente dai file system Unix originari.
- **ext3:** Rappresenta un'evoluzione di `ext2` con l'aggiunta del **journaling** (una tecnica che registra in un log le modifiche non ancora consolidate, prevenendo la corruzione dei dati in caso di interruzioni improvvise).
- **ext4:** È un ulteriore potenziamento di `ext3`. Le sue caratteristiche chiave sono:
    - Capacità di gestire **singoli file** con dimensioni superiori a **2 TB**.
    - Supporto per volumi **file system** più grandi di **16 TB**.
    - Pieno supporto nativo per gli i-node (memorizzati in strutture apposite all'interno del file system).

>[!warning] Compatibilità con Windows (File System FAT)
>
>Linux è progettato per essere versatile: permette infatti di leggere e scrivere dati su file system non nativi, come quelli utilizzati da Windows (es. NTFS o FAT).
>
>Nel caso specifico dell'interazione con il file system **FAT**, si pone un problema strutturale: **FAT non supporta e non memorizza gli i-node** sul disco. Per superare questo ostacolo, Linux adotta un espediente: quando apre un file su una partizione FAT, il sistema operativo **crea gli i-node "on-the-fly" (al volo)** all'interno di una memoria cache temporanea, permettendo al kernel di gestire il file come se si trovasse su un normale file system nativo.
