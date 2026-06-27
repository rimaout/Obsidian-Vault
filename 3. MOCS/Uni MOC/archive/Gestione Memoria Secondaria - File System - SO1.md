---
type: Uni Note
class:
  - "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2026-06-25T19:53
updated: 2026-06-27T13:10
---
## Introduzione

Il Sistema Operativo (SO) ha il compito di gestire i file e di soddisfare le operazioni effettuate dall'utente su di essi. Per fare ciò, un SO deve essere in grado di:
- **Decidere dove posizionare** le strutture richieste dai file sul supporto di memorizzazione.
- **Mantenere traccia** di dove sono state posizionate le informazioni di ciascun file. traccia di dove sono state posizionate le informazioni di un file

>[!warning] Allocazione di un File
>
>I file si allocano in **blocchi**. L'unità minima fisica del disco è il **settore**, ma il SO raggruppa i settori in blocchi (una sequenza contigua di settori del disco).
>
>> **Esempio:** Se dobbiamo salvare un file anche di un solo carattere, il SO allocherà comunque un intero blocco. Lo spazio rimanente nel blocco andrà sprecato (**frammentazione interna**).

Esistono diversi modi per gestire l'allocazione di un file, che variano in base a tre scelte:
- [[#Preallocazione vs. Allocazione Dinamica]]
- [[#Dimensione dei Blocchi]]
- [[#Metodi di Allocazione (contigua, concatenata, indicizzata)]]
  
In oltre l'OS ha il compito di [[#Gestione Spazio Libero]], determinano dove è possibile salvare i file e gestendo la frammentazione.
  
## Preallocazione vs. Allocazione Dinamica

Questa scelta definisce _quando_ e _come_ viene stabilita la dimensione del file sul disco.

>[!note] Preallocazione
>
>Richiede che la **dimensione massima** del file sia dichiarata esplicitamente al momento della sua creazione.
>
>- ***Il problema:*** Nella maggior parte delle applicazioni comuni è difficile stimare lo spazio finale. Gli utenti e le applicazioni tendono a **sovrastimare la dimensione** per essere sicuri di poter memorizzare tutti i dati.
>- ***Risultato:*** Si verifica un forte **spreco di spazio su disco**, a fronte di un risparmio computazionale minimo per il SO.

>[!note] Allocazione Dinamica
>
>La dimensione del file non è fissa, ma viene **aggiustata dinamicamente** nel tempo in base alle operazioni di `append` (aggiunta di dati) o `truncate` (taglio/riduzione del file). È la strategia quasi sempre preferita nei sistemi moderni.

## Dimensione dei Blocchi

>[!note] Porzioni Grandi e di Dimensione Variabile
>
>Il SO assegna al file pezzi di disco grandi e interamente contigui.
>
>- **Vantaggi:** La tabella di allocazione rimane piccolissima (servono pochissime informazioni per tracciare il file). L'accesso sequenziale ai dati è velocissimo perché la testina del disco legge tutto di fila.
>- **Svantaggi:** Gestione dello spazio libero complessa. Quando i file vengono cancellati, si creano "buchi" di diverse dimensioni sul disco (**frammentazione esterna**). Servono algoritmi ad hoc per cercare lo spazio adatto.

>[!note] Porzioni Fisse e Piccole
>
>Il SO assegna lo spazio un blocco alla volta (tipicamente 1 porzione = 1 blocco). I blocchi di un singolo file possono essere sparsi ovunque sul disco.
>
>- **Vantaggi:** Gestione dello spazio libero semplicissima. Non serve compattare il disco: basta consultare una **bitmap** (tabella di bit) dove ogni bit indica se un blocco è libero (0) o occupato (1). Massima facilità di riuso dei blocchi.
 >- **Svantaggi:** Il file risulta frammentato sul disco, rallentando l'accesso sequenziale. Inoltre, porzioni piccole significano tabelle di allocazione enormi, aumentando l'**overhead** (il consumo) di memoria del sistema.

## Metodi di Allocazione (contigua, concatenata, indicizzata)

Esistono 3 principali metodi per l'allocazione dei file
- Contiguo
- Concatenato
- Indicizzato

Tutti e ***necessitano di una tabella di allocazione dei file***, e devono rispettare le seguenti condizioni:

| |**Contiguous**|**Chained**|**Indexed (Fixed)**|**Indexed (Variable)**|
|---|---|---|---|---|
|**Preallocation?**|Necessary|Possible|Possible|Possible|
|**Fixed or variable size portions?**|Variable|Fixed blocks|Fixed blocks|Variable|
|**Portion size**|Large|Small|Small|Medium|
|**Allocation frequency**|Once|Low to high|High|Low|
|**Time to allocate**|Medium|Long|Short|Medium|
|**File allocation table size**|One entry|One entry|Large|Medium|

#### Allocazione Contigua (Contiguous Allocation)

Prevede che a ogni file sia assegnato un insieme di blocchi **consecutivi** sul disco. Richiede necessariamente la preallocazione (dobbiamo sapere in anticipo quanto spazio servirà).

>[!note] File Allocation Table (FAT)
>La struttura della tabella è estremamente semplice. Per ogni file basta **una sola voce (entry)** contenente due informazioni:
>- L'indirizzo del blocco di partenza.
>- La lunghezza totale del file (in blocchi).

>[!danger] Limite - Frammentazione Esterna
>Quando i file vengono cancellati, si creano dei "buchi" vuoti sul disco. Se i buchi sono sparsi, potremmo avere molto spazio libero totale, ma non abbastanza spazio _contiguo_ per un nuovo file.
>   - _Esempio:_ Se un file necessita di **8 blocchi contigui**, e sul disco ci sono 10 blocchi liberi ma isolati (es. 4 da una parte e 6 dall'altra), il file non può essere salvato.
>
>>[!note] Soluzione (costosa) - Compattazione
>>Per risolvere il problema, il SO deve spostare fisicamente tutti i file esistenti per unirli, creando un unico grande blocco vuoto alla fine del disco.
>   > 
>> >⚠️ **Nota:** La compattazione modifica radicalmente la tabella di allocazione (cambiano tutti gli indirizzi di partenza dei file spostati) ed è un'operazione **estremamente onerosa** ancora oggi, a causa dell'enorme quantità di operazioni di I/O richieste.

#### Allocazione Concatenata (Chained / Linked Allocation)

I blocchi di un file possono essere sparsi ovunque sul disco. Non è richiesta alcuna preallocazione: il file può crescere dinamicamente un blocco alla volta.

- **Come funziona:** Ogni blocco contiene i dati dell'utente e, negli ultimi byte, un **puntatore (pointer)** che indica l'indirizzo del blocco successivo.
- **Frammentazione:** La frammentazione esterna è azzerata (qualsiasi blocco libero può essere usato). La frammentazione interna è ridotta al minimo (può verificarsi solo nell'ultimo blocco del file).

>[!note] File Allocation Table (FAT)
>
>Anche qui la struttura della tabella e molto semplice, serve **una sola entry** per file, che punta esclusivamente al primo blocco (il blocco di partenza).

>[!danger] Limite - Accesso Casuale
>- Questa allocazione è ottima per l'accesso **sequenziale** (es. riprodurre un file audio).
>- Pessima per l'accesso **casuale/diretto**: se voglio leggere il blocco numero 50, non posso calcolarne la posizione. Devo obbligatoriamente leggere il blocco 1, seguire il puntatore al blocco 2, poi al 3, e così via, fino al 50.

>[!note] Operazione di Consolidamento
>
>In questo metodo non serve la compattazione per recuperare spazio. Si esegue invece il **Consolidamento** (deframmentazione).
>    - _Cosa fa:_ Sposta i blocchi dello stesso file per renderli fisicamente contigui sul disco.
>    - _Scopo:_ **Non serve a guadagnare spazio**, ma unicamente a migliorare le prestazioni di lettura, riducendo i movimenti della testina del disco.
#### Allocazione Indicizzata (Indexed Allocation)

È la strategia più evoluta e utilizzata (alla base dei file system moderni). Risolve il problema dell'accesso lento dell'allocazione concatenata, eliminando la frammentazione esterna della contigua.

![[Pasted image 20260626160711.png]]

>[!note] Index Block
>Ogni file possiede un blocco speciale chiamato *blocco indice*, all'interno di questo blocco non ci sono dati, ma un **vettore di puntatori** a tutti i blocchi reali del file.
>- _Esempio:_ La tabella dice che il File B ha l'indice al blocco 24. Andando al blocco 24, troveremo una lista ordinata: `[1, 8, 3, 14, 28]`. Questi sono i blocchi che contengono i veri dati del file.
>
>**Gestione dei file grandi (Multi-livello):** Se un file è enorme e i suoi puntatori non entrano in un solo blocco indice, il SO usa schemi a più livelli (indici indiretti, doppi indiretti, ecc.), esattamente come gli _inode_ di Linux.

^231a78

>[!note] La file allocation table (FAT) 
>
>La tabella di allocazione dei file, contiene un'unica entry per file che punta al [[#^231a78|blocco indice]] del file . 

## Gestione Spazio Libero

Oltre a tracciare lo spazio occupato dai file, il Sistema Operativo (SO) deve sapere costantemente dove si trova lo spazio libero sul disco per poter salvare nuovi dati.

Per fare questo, il SO utilizza una **tabella di allocazione del disco** (da affiancare alla tabella di allocazione dei file - FAT). Questa tabella deve essere aggiornata ogni volta che un file viene allocato (creato/ingrandito) o deallocato (cancellato).

Esistono quattro metodi principali per gestire lo spazio libero:
- [[#Tabelle di Bit (Bit Vector / Bitmap)]]
- [[#Porzioni Libere Concatenate (Linked Free Space List)]]
- [[#Indicizzazione]]

#### Tabelle di Bit (Bit Vector / Bitmap)

Lo spazio libero viene rappresentato tramite un vettore in cui ogni singolo bit corrisponde a un blocco sul disco.
- **0** = Blocco libero
- **1** = Blocco occupato
- **Vantaggi:** È compatibile con tutti gli schemi di allocazione dei file e minimizza lo spazio richiesto per la tabella.
- **Svantaggi:** Quando il disco è quasi pieno, la ricerca di un bit "0" diventa lenta, costringendo il SO a scorrere l'intera tabella.
- **Soluzione:** Si utilizzano tabelle riassuntive che coprono porzioni della tabella principale, indicando ad esempio il numero totale di blocchi liberi e la quantità di blocchi liberi contigui.

#### Porzioni Libere Concatenate (Linked Free Space List)

Sfrutta un meccanismo simile all'allocazione concatenata dei file. Il sistema mantiene un puntatore alla prima porzione libera, che a sua volta contiene un puntatore alla porzione libera successiva.

- **Vantaggi:** L'overhead di spazio per la tabella è praticamente nullo. Se ci sono zone libere contigue, si risparmia ulteriore spazio indicando solo l'indirizzo di inizio e la lunghezza della porzione. È compatibile con tutti i metodi di allocazione.
- **Svantaggi (Frammentazione):** Se il disco è molto frammentato, le porzioni libere saranno grandi un solo blocco. La lista diventa lunghissima perché non è possibile accorparle indicando una lunghezza maggiore di 1.
- **Svantaggi (Cancellazione):** Cancellare file molto frammentati richiede molto tempo per aggiornare tutti i puntatori della lista.

#### Indicizzazione

Questo metodo tratta lo spazio libero esattamente come se fosse un file, utilizzando un blocco indice per gestirlo.

- **Funzionamento:** L'indice gestisce le porzioni libere come se fossero di lunghezza variabile. La tabella avrà un'entry per ogni porzione libera presente sul disco (indicando inizio e dimensione).
- **Vantaggi:** Offre un'elevata efficienza operativa e si sposa molto bene con tutti i metodi di allocazione dei file visti in precedenza.

#### Lista dei Blocchi Liberi (Free Block List)

Ogni blocco del disco ha un numero sequenziale identificativo, e i numeri dei blocchi liberi vengono salvati in una zona di memoria.

- **Il problema della RAM:** A differenza delle tabelle dei file (che vengono caricate in RAM solo quando un file viene aperto), le informazioni sullo spazio libero devono essere **sempre** disponibili al SO.
- **La soluzione (Pila/Stack):** Il SO carica in RAM solo una porzione di questa lista di numeri. Questa porzione viene gestita tipicamente come una **Pila (Stack)**.
- **Operazioni:** Si usa un'operazione di _pop_ per estrarre un numero (allocare spazio per un file) e una di _push_ per inserire un numero (deallocare spazio dopo una cancellazione).
- **Ricarico:** Quando i numeri nella porzione in RAM finiscono, il SO va a leggere e caricare la porzione successiva dal disco.
- **Alternative:** Questa struttura dati in RAM può essere gestita anche in altri modi, ad esempio tramite una Coda (Queue).

## I Volumi

Un **volume** rappresenta un disco "logico". Non coincide necessariamente con un hard disk fisico, ma costituisce un'astrazione gestita dal Sistema Operativo.

- **Natura del Volume:** Può essere una singola partizione di un disco fisco, oppure l'unione di più dischi fisici visti come un'unica entità (grazie a sistemi come l'**LVM** - _Logical Volume Manager_). Un volume può anche nascere dalla fusione di più volumi più piccoli (vedi: [[Raid - SO1#Dischi Multipli|Dischi Multipli]]).
- **Astrazione dei Settori:** È un insieme di settori della memoria secondaria a disposizione di SO e applicazioni. Anche se i settori fisici non sono contigui sul disco, l'astrazione del volume li fa apparire come una sequenza perfettamente **contigua**.

## Dati, Metadati e Consistenza

All'interno del file system operiamo una distinzione fondamentale tra due tipi di informazioni:
- **Dati:** Il contenuto effettivo del file (es. il testo di un documento, i pixel di una foto).
- **Metadati:** Le informazioni strutturali gestite dal SO per controllare il file (es. lista dei blocchi liberi, puntatori ai blocchi del file, date di creazione/modifica, permessi e proprietario).
    
>[!note] Il problema della Consistenza
>
>I dati e i metadati devono persistere sul disco, ma per ragioni di performance vengono caricati e modificati anche in **RAM**. Aggiornare costantemente il disco a ogni singola modifica in RAM sarebbe estremamente inefficiente (generando troppe operazioni di I/O). Per questo motivo, il SO sincronizza la RAM sul disco **periodicamente** (ad esempio quando il sistema è in idle o quando si accumulano molte modifiche).
>
>>***Cosa succede in caso di evento imprevisto?***
>>
>>Se il computer si spegne all'improvviso o un disco rigido viene rimosso senza la procedura di espulsione sicura, i metadati sul disco potrebbero non essere aggiornati rispetto alla RAM, creando un'**inconsistenza**.

#### Il Bit di Shutdown (Dirty Bit)

I file system tradizionali scrivono un bit speciale all'inizio del disco per indicare se il sistema è stato arrestato correttamente.
- Al reboot, se il SO legge che il bit è **0 (o "dirty")**, significa che c'è stato un crash.
- Il SO lancia un **programma di ripristino del disco** (come _fsck_ su Linux o _chkdsk_ su Windows) che esegue i seguenti controlli automatici:
    - *Blocco marcato come in uso, ma non appartiene a nessun file?* Viene liberato.
    - *Blocco marcato come libero, ma un file punta a lui? Viene assegnato ufficialmente a quel file.

#### Il Journaling

Il metodo del bit di shutdown costringe il SO a scansionare l'intero disco al riavvio, un'operazione lunghissima sui dischi moderni molto capienti. I file system moderni risolvono questo problema alla radice usando il **Journaling**.

Il Journal (o log) è una zona dedicata del disco in cui il SO annota le operazioni che ha intenzione di compiere **prima** di eseguirle effettivamente sui file e sui metadati reali.

Se al reboot il bit di shutdown indica un crash, il SO non deve scansionare tutto il disco: gli basta consultare il log.
- **Crash durante la scrittura nel File System:** Se l'operazione nel journal era già stata registrata come "completa", il SO legge il log e applica le modifiche interrotte sul file system, recuperando l'errore.
- **Crash durante la scrittura nel Journal:** Se il crash avviene mentre il SO stava scrivendo nel log, l'operazione viene semplicemente scartata e il file system rimane integro allo stato precedente.

>[!note] Tipologie di Journaling
>
>- **Journaling Fisico:** Il SO copia nel journal **tutti i blocchi** che dovranno essere modificati (sia i metadati che i dati reali del file). In caso di crash, basta ricopiare i blocchi dal journal al file system. È il metodo più sicuro in assoluto, ma anche il più lento.
   > 
>- **Journaling Logico:** Il SO copia nel journal **solo i metadati** delle operazioni. È molto più veloce, ma c'è un rischio: se il crash avviene mentre i dati reali si stanno ancora scrivendo sul disco, la struttura del file system si salva (i metadati rimangono coerenti), ma il contenuto effettivo del file potrebbe andare perso o corrompersi.

## Alternative al Journaling

I file system non usano tutti il journaling, esistono altre strategie avanzate per garantire la consistenza dei dati:

>[!note] Soft Updates
>
>Invece di usare un log separato, questo metodo **riordina la sequenza delle operazioni di scrittura** direttamente sul file system. L'algoritmo garantisce che non si creino mai inconsistenze distruttive (permette solo anomalie minori che non causano mai la perdita di dati o corruzione strutturale).

>[!note] Log-Structured File Systems (LFS)
>
>L'intero file system viene pensato e strutturato come un gigantesco **buffer circolare** (un log continuo). Sia i dati che i metadati vengono scritti esclusivamente in modo sequenziale, sempre alla fine del log. Questo significa che non si sovrascrive mai nulla e che sul disco possono coesistere diverse versioni dello stesso file relative a istanti temporali differenti.

>[!note] Copy-on-Write (CoW) File Systems
>
>Utilizzato da file system moderni come _Btrfs_ o _ZFS_. Questo approccio **evita la sovrascrittura** dei blocchi esistenti. Quando un file viene modificato, i nuovi contenuti vengono scritti in blocchi completamente vuoti del disco. Solo dopo che la scrittura dei dati è andata a buon fine, i metadati vengono aggiornati per puntare ai nuovi blocchi. Se si verifica un crash a metà operazione, il file originale rimane intatto nei vecchi blocchi.