---
type: Uni Note
class:
  - "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2026-06-25T12:24
updated: 2026-06-25T15:26
---
## Dischi Multipli

Quando si hanno a disposizione più dischi si possono prendere due scelte:

>[!note] Trattarli Separatamente
>
>- Windows li mostrerebbe esplicitamente come dischi diversi, con etichette diverse 
>- Linux permette di dire che alcune directory sono in un disco, altre su un altro 
>  
>In entrambi i casi durante l'installazione del sistema operativo, si specificano i deschi e poi non ci si pensa più.
>

>[!note] Trattarli come un Disco Unico
>
>È possibile trattare dischi fisici diversi come un unico disco virtuale, si usano principalmente due tecnologie, a seconda che interessi o meno la sicurezza dei dati:
>- [[#Linux LVM (Logical Volume Manager)]]
>- [[#RAID (Redundant Array of Independent Disks)]]

## Linux LVM (Logical Volume Manager)

- **Cos'è:** Un *modulo* del *kernel Linux* che unisce dischi diversi in un unico grande spazio logico.
- **A cosa serve:** Risolve il problema del "disco pieno". Evita che una singola directory cresca fino a saturare il suo disco mentre altri dischi rimangono vuoti. L'utente non deve preoccuparsi di dove salvare i file.
- **Limiti:** È pensato per pochi dischi e **non offre ridondanza**. Se si rompe un disco fisso, l'intero disco virtuale è a rischio.
## RAID (Redundant Array of Independent Disks)

Tecnologia utilizzata quando, oltre a unire i dischi, si cerca sicurezza e velocità.

>[!note] Obbiettivi
>- **Ridondanza:** Lo stesso dato viene memorizzato su più dispositivi contemporaneamente. Se un disco si rompe, il dato è al sicuro sugli altri. Le modifiche ai file vengono propagate automaticamente su tutti i dischi del vettore.
>- **Performance:** Permette di parallelizzare le operazioni, velocizzando la lettura e la scrittura dei dati.

>[!note] Livelli di gestione
>    - **RAID Hardware:** Il sistema operativo vede l'array come un singolo disco standard e si limita a fare operazioni di `read` e `write`. È il controller fisico del dispositivo che si occupa di gestire la distribuzione e la ridondanza dei dati internamente.
>    - **RAID Software:** È il sistema operativo stesso a farsi carico della gestione dei dischi tramite software (consumando risorse di calcolo della CPU).


### RAID 0 (Striping)

- **Ridondanza:** ***❌ Nessuna*** Non offre alcuna tolleranza ai guasti.
- **Funzionamento:** I dischi sono divisi in **strip** (insiemi di settori). Un insieme di strip sulla stessa riga logica prende il nome di **stripe**. I dati vengono distribuiti ciclicamente tra i dischi.
- **Vantaggi:** **Parallelizzazione pura.** Se un file è diviso su più strip, viene letto o scritto contemporaneamente da dischi diversi, moltiplicando la velocità.
- **Capacità totale:** Somma algebrica delle capacità di tutti i dischi.


![[Pasted image 20260625152314.png|400]]

### RAID 1 (Mirroring)

- **Ridondanza:** **Alta.** Ogni dato viene duplicato fedelmente su un disco specchio.
- **Funzionamento:** Configurato in coppie. Se abbiamo $2N$ dischi fisici, la capacità utile di memorizzazione sarà pari a solo $N$ dischi.
- **Tolleranza ai guasti:** Se si rompe un disco, il sistema continua a funzionare usando la copia. Se si rompono due dischi, il sistema sopravvive **solo se** appartengono a coppie diverse; se si rompono sia il disco principale che il suo rispettivo specchio, i dati sono persi. 

![[Pasted image 20260625152335.png]]

## RAID 2 (Hamming Code)

- **Ridondanza:** A livello di singoli bit, non di intero disco.
- **Funzionamento:** Utilizza i codici di Hamming per rilevare errori su 2 bit e correggerli su un singolo bit. I dischi di overhead necessari per memorizzare il codice sono proporzionali al logaritmo della capacità dei dischi dati.
- **Stato:** **Obsoleto.** Non viene utilizzato nei sistemi moderni poiché i dischi rigidi integrano già nativamente il controllo dell'errore a livello di settore.

![[Pasted image 20260625152418.png]]

## RAID 3 (Bit-Interleaved Parity)

- **Funzionamento:** L'architettura prevede un unico disco dedicato esclusivamente alla memorizzazione della **parità** calcolata bit a bit (tramite operazione logica XOR) sulle stesse posizioni dei dischi dati. Se il numero di bit a `1` è dispari, la parità è `1`; se è pari, la parità è `0`.
- **Tolleranza ai guasti:** Tollera il fallimento di **un singolo disco qualsiasi**.
- **Stato:** Non usato commercialmente, ma fondamentale come concetto propedeutico per i livelli successivi.

![[Pasted image 20260625152517.png]]

## RAID 4 (Block-Level Parity)

- **Funzionamento:** Identico al RAID 3, ma la parità viene calcolata e scritta a livello di **blocchi di memoria** (block) anziché di singoli bit.
- **Limiti:** Offre un ottimo parallelismo in lettura, ma soffre del problema delle **piccole scritture**. Poiché il disco di parità è uno solo ed è dedicato, _ogni singola operazione di scrittura_ su qualsiasi disco dati costringe il sistema ad aggiornare anche il disco di parità, creandovi un forte collo di bottiglia (imbuto prestazionale).

![[Pasted image 20260625152526.png]]

## RAID 5 (Distributed Parity)

- **Funzionamento:** Risolve il collo di bottiglia del RAID 4. Le informazioni di parità **non sono isolate** su un unico supporto, ma vengono distribuite ciclicamente su tutti i dischi dell'array.
- **Vantaggi:** Non essendoci un disco di parità fisso, i carichi di scrittura della parità vengono ripartiti uniformemente su tutti i dischi.
- **Tolleranza ai guasti:** Tollera il fallimento di **1 solo disco**.

![[Pasted image 20260625152534.png]]

## RAID 6 (Dual Distributed Parity)

- **Funzionamento:** Evoluzione del RAID 5 in cui vengono generate due diverse funzioni di parità (chiamate parità $P$ e parità $Q$), distribuite asimmetricamente su tutti i dischi. Richiede un overhead fisso pari allo spazio di 2 dischi.
- **Tolleranza ai guasti:** **Molto alta.** Può sopportare il fallimento simultaneo di **2 dischi qualsiasi**.
- **Performance:** Identico al RAID 5 in lettura. In scrittura presenta invece una **penalità prestazionale (Write Penalty)** di circa il 30% superiore rispetto al RAID 5, dovuta al doppio calcolo e alla doppia scrittura delle parità per ogni blocco aggiornato.

![[Pasted image 20260625152545.png]]

## Riepilogo

I parametri fondamentali usati per valutare le prestazioni e l'affidabilità di una configurazione RAID sono:

- **Parallel Access (Accesso Parallelo):** Tutti i dischi dell'array lavorano in modo sincronizzato per servire una singola richiesta di I/O. Ottimo per trasferire file molto grandi.
- **Independent Access (Accesso Indipendente):** Ogni disco (o sottoinsieme di dischi) può elaborare una richiesta di I/O diversa in modo autonomo. Consente al sistema di soddisfare molteplici richieste di file distinti in contemporanea.
- **Data Availability (Disponibilità dei Dati):** La capacità dell'array di continuare a funzionare e permettere il recupero dei dati in caso di guasto hardware (tolleranza ai guasti).
- **Small I/O Request Rate:** L'efficienza e la velocità del RAID nel rispondere a richieste di lettura/scrittura di file di piccole dimensioni. I sistemi con parità distribuita (RAID 5) o mirroring (RAID 1) offrono tassi migliori rispetto ai sistemi con parità dedicata (RAID 4) che soffrono sui carichi di scrittura frequenti.
 
![[Pasted image 20260625152607.png]]
