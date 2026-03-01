---
type: Uni Note
class:
  - "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related:
completed: false
created: 2026-02-04T14:35
updated: 2026-02-05T16:10
---
>[!danger]
>
>Quello che diremo vale per gli hard drive disk (HDD), non per i solid state disk (SSD).

## Introduzione agli  HDD

![[Pasted image 20260205144942.png|400]]

Un `hdd` è suddiviso in tracce, dove ogni **traccia** è un *percorso intero circolare*.

Le tracce sono suddivise in **settori**, delimitati uno dall'altro con delle aree di "demarcazione" chiamate **Intersector Gaps**.

>[!note] Lettura dei Dati
>
>I **dati** si trovano quindi sulle tracce e sui settori, per leggere e scrivere quindi devo sapere su quale traccia e su quale settore di questa traccia si trovano i dati.
>
>Per *selezionare una traccia* bisogna:
>- Spostare una testina se il disco ha testine mobili (ci focalizziamo su queste)
>- Selezionare una testina se il disco ha testine fisse
>
>Per *selezionare un settore*:
>- Dobbiamo aspettare che il disco ruoti (a velocità costante)
>  
>Se i dati sono tanti, potrebbero essere su più settori o addirittura su più tracce.
>
>>***Note:*** una tipica misura di un settore è 512 bytes

>[!note] Prestazioni
>
>Un’operazione sul disco dipende da molti dettagli:
>
>![[Pasted image 20260205151430.png|600]]
>
>1. Il SO chiede al disco se é libero per essere utilizzato.
>2. Se i dischi hanno più canali (più dischi) aspettare anche che il canale sia libero.
>3. Adesso che siamo nel disco interessato dobbiamo muovere la testina sulla traccia (_seek_).
>4. Aspettare il tempo di rotazione per il settore (_Rotational Delay_)
>5. Trasferimento dati, qui il disco continua a girare ma la testina legge o scrive dati.
>   
>Abbiamo il **tempo di accesso** che é dato dalla somma di:
>
>- **Seek Time** ovvero il tempo di posizionamento della testina sulla traccia
>- **Rotational Delay** ovvero il tempo necessario affinché l’inizio del settore raggiunga la testina.
>- **Tempo di trasferimento**, il tempo richiesto per trasferire i dati che scorrono sotto la testina.
>
>Abbiamo inoltre anche i tempi di:
>
>- *Wait for device*: Il tempo di attesa che il dispositivo sia assegnato alla richiesta
>- *Wait for channel*: Attesa che il sotto dispositivo sia assegnato alla richiesta (ad esempio se ci sono più dischi sullo stesso canale di comunicazione)

## Politiche di Scheduling per il Disco

### FIFO

Le richieste sono servite in modo sequenziale è equo nei confronti dei processi.

Se ci sono molti processi in esecuzione, le prestazioni sono simili allo scheduling random.

![[Pasted image 20260205152816.png|500]]

### Priorità

Politica di scheduling dove i processi hanno una priorità assegnata, e in base a questa si decide l'ordine di accesso al disco.

Con questo tipo di politica l’obiettivo non è ottimizzare il disco, ma raggiungere altri obiettivi.

Quindi non va bene per DBMS.

### LIFO

Politica di scheduling dove il disco è dato al processo più che ha effettuato la richiesta più recentemente.

Utile quando:
- se si tratta dello stesso utente, probabilmente sta accedendo sequenzialmente ad un file quindi, è più efficiente mandare avanti lui
- Ottimo per DBMS con transazioni

### SSTF (Shortest Seek Time First)

Politica di scheduling utilizzata per la gestione delle richieste di I/O nei dischi rigidi. Questo approccio mira a ottimizzare le prestazioni minimizzando il tempo di ricerca della testina del disco.

É necessario conoscere la posizione della testina per determinare l'ordine corretto di operazioni per ridurre il movimento della testina.

![[Pasted image 20260205160512.png|500]]

## SCAN

Anche noto come algoritmo "Elevator", è un metodo di scheduling dei dischi per ottimizzare l'accesso alle richieste di lettura e scrittura nei dischi rigidi.

Si scelgono le richieste in modo tale che il braccio si muova sempre in un verso, e poi torni indietro

>***Nota:*** movimento simile al funzionamento di un ascensore.

Caratteristiche:
- *Niente starvation* delle richieste
- *Poco Fair*

Poco Fair perché favorisce le le richieste che si trovano nelle vicinanze della testina, e specialmente quelle vicino ai **bordi** del disco (visto che questo movimento porta la testina a spende più tempo lungo i bordi).

![[Pasted image 20260205160554.png|500]]

## C-SCAN

Politica di Scheduling simile a SCAN ma che è **fair**.

Per fare ciò nella marcia indietro non si accettano richieste.

![[Pasted image 20260205160840.png|500]]

## FSCAN

Politica di Scheduling che evolve SCAN rendendolo **fair**, introducendo due code anziché una sola.

