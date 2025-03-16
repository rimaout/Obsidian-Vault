---
type: Uni Note
class: "[[Reti (class)]]"
academic year: 2024/2025
related: 
completed: true
created: 2025-03-13T10:21
updated: 2025-03-13T10:21
---
## Introduzione

Un argomento di cui si parla spesso nell’ambito delle reti è la velocità della rete o di un collegamento, ovvero quanto velocemente si riesce a trasmettere e ricevere i dati.  In realtà, il concetto di velocità è molto ampio e coinvolge vari fattori che influiscono sulle prestazioni di una rete.

Nel caso di una **rete a commutazione di pacchetto**, le metriche che ne determinano le prestazioni si misurano in termini di:

- [[#Ampiezza di Banda (Rate)]]
- [[#Bandwidth e Bit Rate]]
- [[#Throughput]]
- [[#Ritardi e Perdite di Pacchetti]]

---
## Ampiezza di Banda

Con il termine ampiezza di banda si indicano due concetti leggermente diversi ma strettamente legati:

>[!note] Caratterizzazione del canale o del sistema trasmissivo
>
>In questo caso l'**ampiezza di banda** (espressa in `hertz`) rappresenta l’**intervallo di frequenze** che un mezzo fisico consente di trasmettere senza danneggiare il segnale in maniera irrecuperabile.
>
>Maggiore è l’ampiezza di banda, maggiore è la quantità di informazione che può essere veicolata attraverso il mezzo trasmissivo.

^84c481

>[!note] Caratterizzazione di un collegamento
>
>In questo caso l'**ampiezza di banda** (espressa in `bps`) rappresenta il **transmission rate** (velocità di trasmissione), anche detto "rate", ovvero la quantità di bit al secondo (`bps`) che un link (collegamento tra due nodi) garantisce di trasmettere.
>
>**FORSE È ANCHE DETTO BIT RATE**

---
## Bandwidth e Bit Rate

>[!note] Bit Rate
>
>Il bit rate indica la trasmissione in bit al secondo (`bps`) di un link (collegamento tra due nodi). Questo dipende sia dalla [[#^84c481|banda (in hertz)]] che dalla specifica tecnica di trasmissione, o formato di modulazione digitale utilizzato.
>
>>***oss:*** Il bit rate è proporzionale alla banda in hertz.

>[!note] Bandwidth
>
>Con bandwidth si intende la banda di una rete si intende il bit rate garantito (nominalmente) dai suoi link.

---
## Throughput

Il throughput indica quanto velocemente riusciamo ***effettivamente*** a inviare i dati tramite una rete. 

Rappresenta il numero di bit al secondo (`bps`) che passano attraverso un punto della rete.

>[!warning] Rate vs Throughput
>
>Il rate è una misura della potenziale velocità di un link, il throughput è una misura dell’effettiva velocità di un link (quanto velocemente riusciamo a inviare i dati in realtà).
>
>Un link può avere un rate di `R` bps, ma possiamo inviare solo `T` bps (throughout) tramite
quel link, con `T ≤ R`.

>[!note] Bottleneck
>
>In un percorso da una sorgente a una destinazione un pacchetto può passare attraverso numerosi link, ognuno con throughput diverso.
>
>Il Throughput del intero percorso è uguale al throughput del link con throughput più basso.
>
>![[Pasted image 20250311121226.png|600]]
>
>La situazione reale in Internet è che i dati normalmente passano attraverso due reti di accesso e la dorsale Internet. La dorsale ha un throughput molto alto, quindi il throughput viene definito come il minimo tra i due link di accesso che collegano la sorgente e la destinazione alla dorsale.

>[!note] Throughput nei link condivisi
>
>Il link tra due router non è sempre dedicato a un flusso di dati, ma raccoglie il flusso da varie sorgenti e/o distribuirlo a varie destinazioni.
>
>![[Pasted image 20250228143551.png|700]]
>
>Quindi il rate del link tra i due router è condiviso tra i flussi di dati, in queste esempio la velocità del link principale nel calcolo del throughput è solo 200 kbps in quanto il link è condiviso.

---
## Ritardi (Delay)

La **latenza (ritardo o delay)** è quanto tempo necessario affinché un pacchetto arrivi completamente a destinazione dal momento in cui il primo bit parte dalla sorgente.

Se il tasso di arrivo dei pacchetti in un router è superiore al tasso di uscita allora i pacchetti si accodano nei buffer di attesa.

Abbiamo 4 fattori che contribuiscono ai ritardi:

>[!note] Ritardo di Elaborazione (processing delay)
>
>Ritardi dovuti ad operazioni effettuate sui pacchetti prima della trasmissione (controllo errori sui bit, determinazione del canale di uscita).

>[!note] Ritardo di Accodamento (queuing delay)
>
>Ritardo dovuto all'attesa di trasmissione dovuta alla coda el router, può variare da pacchetto a pacchetti.
>
>Il calcolo si basa su misure statistiche e dipende strettamente dall'intesità di traffico:
>
>$$
>\text{Intensità di Traffico} = \frac{{L \cdot a}}{R}
>$$
>
>Dove:
>- `R`: Rate di trasmissione (`bps`)
>- `L`: lunghezza del pacchetto (`bit`)
>- `a`: tasso medio di arrivo dei pacchetti (`pkt/s`)
>
>**Ritardo:**
>- $\textcolor{orange}{\text{Intensità di Traffico} \sim 0}$: poco ritardo
>- $\textcolor{orange}{\text{Intensità di Traffico} \to 0}$: (tende a 1) il ritardo si fa consistente
>- $\textcolor{orange}{\text{Intensità di Traffico} > 1}$: più “lavoro” in arrivo di quanto possa essere effettivamente svolto, ritardo medio infinito!

>[!note] Ritardo di Trasmissione (transmission delay)
>
>Tempo richiesto dal nodo per trasmettere (immettere) tutti i bit del pacchetto sul collegamento (rete)
>
>Se il primo bit del pacchetto viene trasmesso al tempo `t1` e l’ultimo bit del pacchetto viene messo in linea al tempo `t2`, il ritardo di trasmissione del pacchetto è (`t2-t1`).
>
>**Algoritmo:** Pacchetti trasmessi in First-come-first-served
>
>**Calcoli:** 
>- `R = rate del collegamento (in bps)`
>- `L = lunghezza del pacchetto (in bit)`
>- `Ritardo di trasmissione = L/R`

>[!note] Ritardo di Propagazione (propagation delay)
>
>Tempo che un bit impiega per propagarsi sul collegamento (viaggiare dal punto `A` al punto `B`)
>
>**Calcoli:**
>- `d = lunghezza del collegamento fisico`
>- `s = velocità di propagazione del collegamento`
>- `Ritardo di propagazione = d/s`
>  
>>***oss:*** Velocità di propagazione solitamente è ~2x108 m/sec ovvero la velocità della luce.

### Ritardo Totale Nodo

>[!note] Ritardo di Nodo
>
>Il ritardo di nodo rappresenta tutti i ritardi che possono affliggere un nodo:
>
>$$
>d_{\text{nodo}} = d_{\text{proc}} + d_{\text{queue}} + d_{\text{trans}} + d_{\text{prop}}
>$$
>
>Dove:
>- $d_{\text{proc}}$: ritardo di elaborazione (processing delay)
>- $d_{\text{queue}}$: ritardo di accodamento (queuing delay)
>- $d_{\text{trans}}$: ritardo trasmissione (transmission delay)
>- $d_{\text{prop}}$: ritardo di propagazione (propagation delay)
>
>![[Pasted image 20250313081017.png|600]]

### Rate x Ritardo

Il massimo numero di bit che possono riempire un collegamento è rappresentato dal calcolo $\text{rate} \cdot \text{ritardo}$

Dove con `ritardo` ritardo si intende il [[#Ritardo Totale Nodo|ritardo totale di un nodo]].

>[!example] Esempio
>
>Supponiamo di avere un link con rate di 1 bps e un ritardo di 5 secondi, allora non possono esserci più di 5 bit contemporaneamente sul link.
>
>![[Pasted image 20250313100858.png|400]]

---
## Perdita di Pacchetti (packet loss)

Se una coda (detta anche buffer) ha capacità finita quando il pacchetto trova la coda piena, viene scartato (e quindi va perso)

Il pacchetto perso può essere ritrasmesso dal nodo precedente, dal sistema terminale che lo ha generato, o non essere ritrasmesso affatto.

---
## Trace Route

**Traceroute (tracert)**: programma diagnostico che fornisce una misura del ritardo dalla sorgente a tutti i router lungo il percorso Internet punto-punto verso la destinazione, funzionamento:

- invia gruppi di tre pacchetti, ogni gruppo con tempo di vita incrementale (da 1 a n, massimo valore = 30) che raggiungeranno il router i (i=1,n) sul percorso verso la destinazione
- il router i restituirà i pacchetti al mittente
- il mittente calcola l’intervallo tra trasmissione e risposta

L’output presenta 6 colonne:
1. Il numero di router sulla rotta
2. Nome del router
3. Indirizzo del router
4. tempo di andata e ritorno 1° pacchetto
5. tempo di andata e ritorno 2° pacchetto
6. tempo di andata e ritorno 3° pacchetto

Se la sorgente non riceve risposta da un router intermedio (o ne riceve meno di 3) allora pone un asterisco al posto del tempo RTT.

Tempo di andata e ritorno (*round trip time - RTT*) ed include i 4 ritardi visti precedentemente.

![[Pasted image 20250313095825.png|700]]

