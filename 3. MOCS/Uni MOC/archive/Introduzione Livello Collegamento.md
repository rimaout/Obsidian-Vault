---
type: Uni Note
class: "[[Reti (class)]]"
academic year: 2024/2025
related: 
completed: true
created: 2025-06-09T08:54
updated: 2025-06-11T17:20
---
## Livelli visti fino ad ora

Riassunto della comunicazione nei vari livelli dello stack:
- **Applicazione** - I due utenti possono immaginare che tra di essi esista un *canale logico bidirezionale* attraverso il quale si possono inviare messaggi. Ma in realtà la comunicazione avviene attraverso più livelli.
- **Trasporto** - I protocolli di trasporto forniscono la *comunicazione logica* tra processi di host differenti, permettendo agli host di seguire i processi come se fossero direttamente connessi.
- **Rete** - *Comunicazione host-to-host*
- **Collegamento** - La *comunicazione* avviene *hop-to-hop* o nodo-to-nodo. I protocolli a livello di collegamento si occuperanno del trasporto di datagrammi lungo un singolo canale di comunicazione.

>[!note] Collegamento Terminologia
>
>Quando si è nel contesto del livello di collegamento si utilizzano i seguenti termini:
>- *Host* e *Router* prendono il nome di **nodi o stazioni**
>- I canali di comunicazione si chiamano **collegamento o link**:
>    - Collegamenti cablati
>    - Collegamenti wireless
>    - LAN
>- Le unità di dati scambiate dai protocolli a livello di link sono chiamate **frame**.

>[!note] Dov'è implementato?
>
>Deve essere implementato in tutti gli host e viene realizzato con un adattatore ovvero la **Network Interface Card** (NIC), questa implementa sia il livello di collegamento che quello fisico.
>
>Realizzata attraverso una combinazione di hardware, software e firmware.

## Collegamento o Link

I nodi all’interno di una rete sono fisicamente collegati da un mezzo trasmissivo come un cavo o l’aria.

E’ possibile utilizzare:
- un **collegamento punto-punto** ovvero quando si sfrutta l’intera capacità del mezzo dedicato a due soli dispositivi.
- un **collegamento broadcast** ovvero quando il mezzo trasmissivo è condiviso tra varie coppie di dispositivi.

Passando da un collegamento ad un altro, un datagramma può essere gestito da diversi protocolli e non tutti i protocolli a livello di trasporto offrono gli stessi servizi.

## Servizi

>[!note] Framing
>
>I protocolli incapsulano i datagrammi del livello di rete all’interno di un frame a livello di link.
>
>Per identificare origine e destinazione vengono utilizzati indirizzi **MAC**.

>[!note] Consegna affidabile
>
>É una consegna dei frame basata su ACK (come nel livello di Trasporto), non è sempre utilizzata, soprattutto nelle reti a basso tasso di errore come quelle cablate. È quindi più facile vederla su reti wireless.

>[!note] Controllo di flusso
>
>Evita che il nodo trasmittente saturi quello ricevente.

>[!note] Rilevazione di errori
>
>Gli errori sono causati dalle interferenze, il nodo ricevente è in grado di rilevare errori tramite l’inserimento di bit di “parità” (controllo) nel frame da perte del mittente.

>[!note] Correzione degli errori
>
>Il nodo ricevente, grazie all'utilizzo di bit di parità, determina il punto in cui si è verificato l’errore, e lo corregge.

Questi servizi possono essere divisi in servizi effettuati dal mittente e dal ricevente:

Da parte del lato **mittente**:
- Incapsula i datagrammi in un frame
- Imposta il bit rilevazione degli errori, trasferimento affidabile, controllo di flusso etc…
  
Da parte del lato **ricevente**:
- Estrae i datagrammi e li passa al nodo ricevente
- Individua gli errori, trasferimento dati affidabile, controllo di flusso etc…

## DLC e MAC

Il **Data-Link Control (DLC)** si occupa di tutte quelle procedure per la *comunicazione tra due nodi adiacenti* (comunicazione nodo-a-nodo), indipendentemente dal fatto che il collegamento sia dedicato o broadcast:
- Framing
- Controllo del flusso e degli errori
- Rilevamento e correzione degli errori

Il **Media Access Control (MAC)** si occupa degli aspetti dei canali broadcast, più precisamente del controllo dell’accesso al mezzo condiviso.

![[Pasted image 20250609094440.png|800]]

## Errori

Gli errori sono dovuti a interferenze che possono cambiare la forma del segnale.

Molto spesso le interferenze coinvolgono più di un bit, questo perché la probabilità che avvenga un errore di tipo **burst** (a raffica) è più elevata rispetto a quella di un singolo bit in quanto la durata dell’interferenza (rumore) normalmente è più lunga rispetto a quella di un solo bit.

![[Pasted image 20250609095320.png|1000]]

>[!example] Esempio
>Più precisamente il numero di bit coinvolti dipende dalla velocità di trasferimento dati e dalla durata del rumore, ad esempio: 
>- $\text{Velocità trasmissione} = 1\, kps$
>- $\text{Durata rumore} = 1/100\, s$
>
>Numero possibile di bit influenzati è:
>$$
>\begin{align*}
>\text{velocità trasmissione} \times \text{durata rumore} = 1kps \times \frac{1}{100}s = 1000 \frac{bit}{s} :  100s = 10\, bit
>
>\end{align*}
>$$

### Rilevazione degli errori

![[Pasted image 20250609095554.png|850]]

Indichiamo:
- **EDC** - Error Detection and Connection
- **D** - Dati che devono essere protetti da errori e ai quali vengono aggiunti dei bit EDC

Da notare che la rilevazione degli errori non è affidabile al 100%:
- Potrebbero esserci errori non rilevati
- Per ridurre la probabilità della mancata rilevazione di solito si usa un’elevata **ridondanza**

>[!note] Parity Bit
>
>È un bit aggiuntivo che viene scelto in modo da rendere pari il numero totale di 1 all’interno della codeword:
>- Se si usa un **unico bit di parità** possiamo sapere soltanto che si è verificato almeno un errore in un bit.
>- Se si usa una **parità bidimensionale** allora possiamo individuare e correggere gli errori
>
>![[Pasted image 20250609095850.png|550]]
