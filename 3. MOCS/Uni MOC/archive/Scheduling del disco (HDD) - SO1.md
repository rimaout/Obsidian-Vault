---
type: Uni Note
class:
  - "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2026-02-04T14:35
updated: 2026-06-25T12:24
---
>[!danger] Attenzione
>
>Queste informazioni valgono solamente per gli **hard drive** disk (HDD), non per i solid state disk (SSD).

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

Con questo tipo di politica l’obiettivo non è ottimizzare il disco, ma raggiungere altri obiettivi, quindi:
- non va bene per DBMS.

### LIFO

Politica di scheduling dove il disco è dato al processo che ha effettuato la richiesta più recentemente.

Utile quando:
- se si tratta dello stesso utente, probabilmente sta accedendo sequenzialmente ad un file quindi, è più efficiente mandare avanti lui
- ottimo per DBMS con transazioni

### SSTF (Shortest Seek Time First)

Politica di scheduling utilizzata per la gestione delle richieste di I/O nei dischi rigidi. Questo approccio mira a ottimizzare le prestazioni minimizzando il tempo di ricerca della testina del disco.

É necessario conoscere la posizione della testina per determinare l'ordine corretto di operazioni per ridurre il movimento della testina.

![[Pasted image 20260205160512.png|500]]

### SCAN

Anche noto come algoritmo "Elevator", è un metodo di scheduling dei dischi per ottimizzare l'accesso alle richieste di lettura e scrittura nei dischi rigidi.

Si scelgono le richieste in modo tale che il braccio si muova sempre in un verso, e poi torni indietro

>***Nota:*** movimento simile al funzionamento di un ascensore.

Caratteristiche:
- *Niente starvation* delle richieste
- *Poco Fair*

Poco Fair perché favorisce le le richieste che si trovano nelle vicinanze della testina, e specialmente quelle vicino ai **bordi** del disco (visto che questo movimento porta la testina a spende più tempo lungo i bordi).

![[Pasted image 20260205160554.png|500]]

### C-SCAN

Politica di Scheduling simile a SCAN ma che è **fair**.

Per fare ciò nella marcia indietro non si accettano richieste.

![[Pasted image 20260205160840.png|500]]

### FSCAN

Politica di Scheduling che evolve [[#SCAN]] rendendolo **fair**, utilizzando due code distinte per separare il lavoro "in corso" da quello "in arrivo".

**Funzionamento:**
0. Si utilizzano due code: la coda **F** (di servizio) e la coda **R** (di raccolta).
1. All'inizio, tutte le richieste da gestire sono in `F`, mentre `R` è vuota.
2. Mentre le richieste in `F` vengono servite utilizzando la politica [[#SCAN]] , _tutte_ le nuove richieste in arrivo vengono aggiunta ad `R`
3. Quando la coda `F` è completamente svuotata, le due code si scambiano i ruoli: `R` diventa la nuova `F` da servire, e si ricomincia.

**Vantaggio:** Questo garantisce _fairness_ (equità), perché nessuna nuova richiesta può ritardare all'infinito quelle vecchie.

**Limite:** Poiché la coda `R` raccoglie _tutte_ le richieste che arrivano mentre si serve `F`, non abbiamo alcun controllo su quanto `R` possa diventare grande. Se `F` impiega molto tempo per essere smaltita, la prima richiesta finita in `R` subirà un tempo di attesa lunghissimo e imprevedibile

### N-step-SCAN

N-step-SCAN è l'evoluzione diretta di [[#FSCAN]]. Risolve il problema del tempo di attesa imprevedibile segmentando le richieste in più code di **dimensione massima prefissata**.

É una generalizzazione della politica di scheduling [[#FSCAN]] con `N > 2` (dove `N` è il numero di code)
- Le nuove richieste in arrivo vengono inserite nella coda i-esima fino al raggiungimento della sua **capienza massima**.
- Una volta piena, le richieste successive vengono deviate nella coda successiva, ovvero la `(i+1) mod N` (modulo `N` serve a ricominciare dalla prima coda quando si arriva all'ultima)
- La testina serve una coda alla volta usando sempre il movimento ottimizzato dello [[#SCAN]]. Durante il servizio, alla coda non viene aggiunta nessuna nuova richiesta.
  
Imponendo un limite al riempimento della singola coda, il sistema garantisce un **tempo di attesa massimo calcolabile** (Bounded Delay). Nessuna richiesta rimarrà bloccata per ore in una mega-coda in continua crescita, rendendo il sistema più reattivo e le attese molto più prevedibili.


