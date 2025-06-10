---
type: Uni Note
class: "[[Reti (class)]]"
academic year: 2024/2025
related: 
completed: false
created: 2025-06-09T10:56
updated: 2025-06-10T20:04
---

## Introduzione

Quando si utilizzano collegamenti broadcast, ovvero mezzi di comunicazione condivisi tra vari host, c'è il rischio che nello svolgimento di comunicazioni in parallelo avvengano collisioni.

Per risolvere questo problema sono stati creati dei protocolli che regolano le trasmissioni sul canale condiviso.

>[!note] Protocollo di accesso multiplo ideale
>
>Dato un canale broadcast con velocità di `R bps`, un protocollo di accesso multiplo ideale è strutturato in questo modo:
>1. Quando un nodo deve inviare dati dispone di un tasso trasmissivo pari a `R bps`
>2. Quando `M` nodi devono inviare dati questi dispongono di un tasso trasmissivo pari a `R/M bps`
>3. Il protocollo è decentralizzato, ovvero non ci sono nodi master e non c’è sincronizzazione dei clock

## Classificazione

I protocolli MAC (Multiple Access Connection) possono essere suddivisi in tre categorie:

>[!note] Channel Partitioning
>
>
>- [[#TDMA (Time Division Multiple Access)]]
>- [[#FDMA (Frequency Division Multiple Access)]]
>- CDMA (Code Division Multiple Access)

>[!note] Random Access
>
>- [[#ALOHA]]
>- [[#Slotted ALOHA]]
>- CSMA/CD
>- CSMA/CA

>[!note] Controlled Acces (taking-turn)
>
>Nei protocolli **a rotazione** ciascun nodo ha il suo turno per trasmettere, chi deve trasmettere di più però avrà turni più lunghi.
>- Reservation
>- Polling
>- Token passing

## Channel Partitions Protocols

Nei protocolli a **suddivisione del canale** il canale è diviso in “parti più piccole” di tempo, frequenza o codice, poi queste parti vengono associate ai nodi per un utilizzo esclusivo, assicurando che *non avvengano collisioni*.
### TDMA (Time Division Multiple Access)

In questi protocolli assegnamo diversi intervalli di tempo ai nodi per comunicare, ogni nodo avrà il suo intervallo. Se uno slot non viene utilizzato allora rimane inattivo.

Il tasso trasmissivo di questa tipologia di protocolli è `R/N bps`, dove:
- `R` è il rate ovvero la velocità di trasmissione espressa in bit al secondo (`bps`)
- `N` è il numero di nodi, ovvero il numero di suddivisioni del collegamento

![[Pasted image 20250609111913.png|700]]

### FDMA (Frequency Division Multiple Access)

Suddividono il canale in bande di frequenza, a ciascun nodo è assegnata una banda di frequenza prefissata.

![[Pasted image 20250609112334.png|700]]

## Random Access Protocols

Ogni nodo non ha controllo sugli altri, quando deve inviare segue delle procedure definite dal protocollo per decide se può spedire o no.

Questi protocolli sono detti ad **accesso casuale**, perché:
- Non è specificato un tempo nel quale il nodo deve trasmettere
- Non ci sono regole su quale sarà il prossimo nodo a trasmettere

Questo significa avviene una **contesa del canale**, ovvero i *nodi competono* tra loro per accedere al mezzo trasmissivo.

Può avvenire che due nodi trasmettano contemporaneamente generando una **collisione**, per questo è importante che sia specificato come:
- Rilevare le collisioni
- Definire come ritrasmettere il segnale se si è verifica una collisione

### ALOHA

È stato il primo protocollo ad accesso casuale proposto, fu sviluppato nelle Hawaii negli anni 70 per permettere la comunicazione delle isole mediante una LAN wireless (è però possibile utilizzare qualsiasi mezzo).

L'ALOHA "puro" si basa su questo funzionamento:
1. Ogni stazione può trasmettere ogni qual volta ha frame da inviare.
2. Il ricevente invia un ACK se riceve correttamente il frame, altrimenti non non risponde.
3. Se il mittente non riceve l'ACK entro un [[#^b8c322|timeout]] allora deve ritrasmettere.
4. Se due nodi ritrasmettono contemporaneamente si verifica una collisione, allora si attende altro tempo random detto [[#^f175f9|backoff]] prima di effettuare la ritrasmissione.
5. Dopo un numero massimo di tentativi `Kmax`​ un nodo interrompe i suoi tentativi di rinvio e prova più tardi.

>[!note] Timeout
>
>Il timeout equivale al massimo ritardo di propagazione di round-trip (andata del frame e ritorno dell’ack) tra le due stazioni più lontane ($2T_{p}$).

^b8c322

>[!note] Back-off
>
>Dopo che è stata confermata una collisione, il mittente aspetta il tempo di `back-off`($T_{B}$) prima di rinviare il frame, la casualità aiuta a ridurre la probabilità di ottenere una nuova collisione.
>
>Il tempo di back-off $T_{B}$ è un valore scelto casualmente che dipende dal numero `k` di trasmissioni fallite.
>
>$$
>T_{B} = R\cdot T_{fr}
>$$
>
>Dove:
>- $R \in [0,\, 2^{k-1}]$
>- $K = \text{Numero tentativi}$
>- $T_{fr} = \text{tempo x invio di frame}$
>- $K_{max} = 15$
>  
>>[!example] Esempio
>>
>>Le stazioni in una rete wireless ALOHA sono a una distanza massima di 600 km. Supponendo che i segnali si propaghino a `3 × 108 m/s`, troviamo:
>>
>>$$
>>T_{p} = (600 \cdot 10^{3}) / (3 \cdot 10^{8}) = 2\text{ms}
>>$$
>>
>>Quindi per `K = 2` l'intervallo di `R` è `{0,1,2,3}`. Ciò significa che $T_{B} = R \cdot T_{fr}$ può essere `0`,`2`,`4` o `6 ms` sulla base del risultato della variabile casuale `R`.

^f175f9

>[!note] Tempo di vulnerabilità
>
>Il tempo di vulnerabilità è intervallo nel quale il frame è a rischio di collisioni e è uguale a:
>
>$$
>\text{Tempo di vulnerabilità}= 2T_{fr}​
>$$
>
>Dove $T_{fr}$ è il tempo di trasmissione di un frame.
>
>  
>![[Pasted image 20250610120720.png|600]]
>
>Il frame trasmesso a `t` si sovrappone con la trasmissione di qualsiasi altro frame inviato in `[t-1,t+1]`.

>[!note] Efficenza (Throuhgput)
>
>L’efficienza è definita come la frazione di slot vincenti in presenza di un elevato numero `N` di nodi attivi, che hanno sempre un elevato numero di pacchetti da spedire.
>
>*Assumiamo* che 
>- tutti i frame hanno la stessa dimensione
>- ogni nodo ha sempre un frame da trasmettere.
>
>*Definiamo* che:
>- `p` è la probabilità che un nodo trasmetta un frame
>- `(1-p)` è la probabilità che un nodo trasmetta un frame
> 
>Se un inizia a trasmettere nel istante di tempo `t0`, perché la trasmissione vada a buon fine, nessun altro nodo deve aver iniziato una trasmissione nel periodo `[t0-1, t0]`, tale probabilità è data da $(1-p)^{N-1}$ (ovvero la probbailita che nessuno dei restanti `n-1` trasmetta).
>
>Allo stesso modo nessun nodo deve iniziare a trasmettere nel tempo `[t0, t0+1]`, e la probabilità di questo evento è ancora $(1- p)^{N-1}$.
>
>La probabilità che un nodo trasmetta con successo è dunque $p(1-p)^{2(N-1)}$
>
>Per calcolare l'efficenza supponiamo di avere un infinito numero di nodi e calcoliamo:
>
>$$
>\lim_{ N \to \infty } p(1-p)^{2(N-1)} = \frac{1}{2e} = 0.18
>$$
>
>Quindi otteniamo che il Il throughput non è `R` ma $0.18\cdot R\text{ bps}$, questo significa che nel caso migliore solo il 18% degli slot svolge un lavoro utile.

### Slotted ALOHA

Un modo per aumentare l’efficienza di ALOHA consiste nel dividere il tempo in intervalli discreti, ciascuno corrispondente ad un frame time ($T_{fr}$).

I nodi devono essere **sincronizzati** tra loro, ovvero devono essere d'accordo nel confine degli intervalli, questo è realizzabile utilizzando un attrezzatura speciale che mette un breve segnale all’inizio di ogni intervallo.

>[!note] Funzionamento
>
>Prima di tutto dobbiamo fare delle **assunzioni**:
>- Tutti i frame hanno la stessa dimensione.
>- Il tempo è suddiviso in slot, questi equivalgono al tempo di trasmissione di un frame.
>- I nodi possono iniziare la trasmissione soltanto all’inizio di uno slot.
>- I nodi sono sincronizzati.
>- Se in uno slot ci sono delle collisioni di pacchetti allora i nodi coinvolti rilevano l’evento prima del termine dello slot.
>
>Adesso vediamo il **funzionamento**,  un nodo prima di spedire un pacchetto attende l’inizio di uno slot e:
>- Se non si verificano collisioni il nodo può trasmettere un nuovo pacchetto allo slot successivo.
>- Se si verificano collisioni allora il nodo ritrasmette con probabilità `p` il pacchetto negli slot successivi.
>  
>![[Pasted image 20250610140800.png|600]]

>[!note] Vantaggi e Svantaggi
>
>I ***vantaggi*** sono:
>- Consente a un singolo nodo di trasmettere continuamente pacchetti alla massima velocità del canale.
>- l **tempo di vulnerabilità** si riduce a un solo slot ($T_{fr}$).
>  
>Gli ***svantaggi*** sono:
>- Una certa frazione degli slot presenterà collisioni e di conseguenza andrà “sprecata”
>- Un’alta frazione degli slot rimane vuota, quindi inattiva.

>[!note] Efficenza (Throuhgput)
>
>Dati `N` nodi con pacchetti da spedire, ognuno trasmette i pacchetti in uno slot con probabilità `p`.
>- La probabilità di successo di un dato nodo è $p(1-p)^{n-1}$
>- La probabilità che ogni nodo abbia successo è $N \cdot p(1-p)^{n-1}$
>
>Per calcolare l'efficenza supponiamo di avere un infinito numero di nodi e calcoliamo:
>
>$$
>\lim_{ N \to \infty } N \cdot  p \cdot  (1-p)^{N-1} = \frac{1}{e} = 0.37
>$$
>
>Quindi otteniamo che il Il throughput non è `R` ma $0.37\cdot R\text{ bps}$, questo significa che nel caso migliore solo il 37% degli slot svolge un lavoro utile.

### CSMA (Carrier Sense Multiple Access)

Il protocollo CSMA sta pre *"Carrier Sense Multiple Access"* ovvero *"Accesso Multiplo a rilevazione della portante"* e prima di trasmettere effettua i seguenti controlli:
- Si pone in ascolto prima di trasmettere (**listen before talk**).
- Se rileva che il canale è libero, trasmette l'intero pacchetto.
- Se il canale sta già trasmettendo, il nodo aspetta un altro intervallo di tempo.

Utilizzando questo tecnica possono ancora **avvenire collisioni**, infatti il ritardo di propagazione fa sì che due nodi potrebbero non rilevare la reciproca trasmissione.

l tempo di vulnerabilità è dato quindi dal tempo di propagazione:

![[Pasted image 20250610185552.png|450]]

- B invia in t0, D ascolta in t1 ma non c'è arriva ancora ninete quindi pena ch eil canale sia libero, quindi inzia ad invaire. ma in realtà A stava invaindo quindi poco dopo s ene accorge.
  
  