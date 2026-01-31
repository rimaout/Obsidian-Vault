---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: true
created: 2025-06-14T16:36
updated: 2026-01-31T13:32
---
## Introduzione

Fanno parte delle reti Wireless:
- LAN Wireless quindi reti WiFi
- Reti Cellulari
- Bluetooth
- Reti di sensori come ad esempio RFID o altri dispositivi smart

>[!note] Elementi delle LAN Wireless
>
>- **Wireless hosts** - Dispositivi mobili (cellulari, laptop) o fissi (PC) che non utilizzano Ethernet ma si connettono in Wi-Fi.
>- **Base station** - Connesse alla rete tramite cavo, permettono il collegamento tra sottoreti wireless e non wireless.
>- **Wireless link** - Collegano tipicamente i dispositivi mobili alle base station; possono inoltre fungere da backbone per interconnettere diverse reti.

>[!note] Caratteristiche LAN Wireless
>
>- Usano l’aria come mezzo trasmissivo, condiviso fra tutti gli host.
>- Gli host non sono fisicamente connessi tramite cavo e possono quindi muoversi liberamente.
>- Collegamento ad altre reti: la base station (**Access Point**) è connessa alle reti cablate.

>[!note] Migrazione da rete cablata a wireles
>
>Il funzionamento di una rete cablata o wireless dipende esclusivamente dai due sottolivelli inferiori dello stack (collegamento e fisico). Per migrare una rete cablata a una wireless è sufficiente:
>1. Sostituire le schede di rete cablate con schede Wi-Fi (o adattatori wireless).
>2. Rimpiazzare lo switch con uno o più Access Point.
>
>In questo modo cambiano soltanto gli indirizzi MAC (livello di collegamento): gli indirizzi IP (livello di rete) restano invariati.
>
>![[Pasted image 20250614164940.png|600]]

>[!note] Reti senza infrastruttura
>
>Una rete peer-to-peer è un insieme di host che si auto-organizzano per formare una rete e comunicano liberamente tra loro.  
>
>Ogni host deve implementare tutte le funzionalità di rete, come:
>- network setup
>- routing
>- forwarding
>- e così via.
>
>![[Pasted image 20250614165106.png|400]]
## Problemi delle reti wireless

**Attenuazione del Segnale** - La potenza di un segnale elettromagnetico diminuisce all’aumentare della distanza dal trasmettitore, perché l’onda si propaga in tutte le direzioni e la sua energia si distribuisce su un volume sempre più ampio.

**Propagazione multi-path** - Quando l’onda incontra un ostacolo, parte dell’energia viene riflessa, diffusa o rifratta. Un medesimo segnale può quindi giungere a destinazione lungo percorsi diversi e con ritardi diversi in funzione del numero di riflessioni subite.

![[Pasted image 20250614171537.png|500]]

**Interferenze** - Si distinguono due casi principali:
1. Un destinatario può ricevere versioni multiple dello stesso segnale dal medesimo trasmettitore a causa della propagazione multi-path.
2. Un destinatario può ricevere segnali sovrapposti provenienti da trasmettitori diversi che operano sulla stessa frequenza.

>[!note] Errori
>
>Tutte queste caratteristiche (attenuazione, multi-path, interferenze) introducono errori nel segnale.
> 
>Per valutare la qualità del collegamento si utilizza il **Signal-to-Noise Ratio** (SNR), cioè il rapporto tra potenza del segnale utile e potenza del rumore di fondo:
> 
>- Se lo SNR è **alto**, il segnale utile è molto più forte del rumore e può essere correttamente demodulato in dati.
>- Se lo SNR è **basso**, il rumore diventa comparabile o superiore al segnale utile, aumentando il tasso di errore e rendendo difficile (o impossibile) il recupero dei dati.

## Controllo dell’accesso al mezzo

Poiché **l’aria è un mezzo condiviso** tra tutti gli host, è necessario controllare l’accesso al canale per evitare collisioni. 

Nel wireless *non è possibile adottare CSMA/CD* come in Ethernet, perché non si può effettuare collision detection con lo stesso metodo, infatti:
- Per rilevare una collisione un host dovrebbe trasmettere e ricevere simultaneamente, ma il segnale in ricezione sarebbe molto più debole di quello trasmesso. Ciò richiederebbe hardware complesso e un consumo di energia elevato, incompatibile con i dispositivi mobili alimentati a batteria.  
- Il costo in termini di complessità e consumo energetico sarebbe proibitivo: si renderebbero necessarie batterie molto più grandi e adattatori di rete sofisticati.  

>[!note] Hidden Terminal Problem
>
>Inoltre esiste il problema del hidden terminal: un host, pur “ascoltando” il canale, potrebbe non accorgersi della trasmissione di un altro host per vari motivi, ad esempio:  
>- Un **ostacolo fisico** che blocca il segnale di un trasmettitore ma non di un altro.  
>- La **distanza** e l’attenuazione che rendono il segnale troppo debole per essere rilevato, pur interferendo con la comunicazione di un ricevitore più vicino.

^8d9266

## IEEE 802.11

IEEE ha definito le specifiche per le LAN wireless con la famiglia 802.11, che copre i livelli di collegamento e fisico:
- Velocità massima: 11 Mbps  
- Banda di frequenza: 2,4–2,5 GHz

Il termine “Wi-Fi” (Wireless Fidelity) è diffusamente usato per indicare le reti basate su 802.11. In realtà, “Wi-Fi” è un marchio registrato e indica una LAN wireless certificata dalla Wi-Fi Alliance, un’associazione no-profit che promuove l’interoperabilità e la diffusione delle reti wireless.

## Architettura BSS (Basic Service Set)

L'architettura Basic Service Set (BSS) è costituita da uno o più host wireless e da un access point.

Si può trovare anche senza AP, ovvero una rete standalone:

![[Pasted image 20250614174214.png|700]]

## Architettura ESS (Extended Service Set)

L'architettura Extended Service Set (ESS) è costituita da due o più [[#Architettura BSS (Basic Service Set)|BSS]] con infrastruttura.

- I *BSS sono interconnessi* tramite un **sistema di distribuzione**, che può essere una rete cablata (ad es. Ethernet) o wireless.
- All’interno dello stesso BSS, due stazioni in campo di vista (in-visibility) comunicano direttamente; stazioni in BSS diversi si scambiano dati tramite l’Access Point (AP).

![[Pasted image 20250614174531.png|700]]

## Canali e Associazione

Lo spettro `2.4GHz` - `2.485GHz` è diviso in 11 canali parzialmente sovrapposti
L’amministratore dell’AP sceglie una frequenza
m Sono possibili interferenze (stesso canale per AP vicini)
m Il numero massimo di frequenza utilizzabili da diversi AP per
evitare interferenze è 3 (usando i canali 1,6,11). I canali non
interferiscono se separati da 4 o più canal

L’architettura IEEE 802.11 prevede che una stazione wireless si associ ad un AP per accedere a Internet.

## Protocollo MAC 802.11

Più stazioni possono voler comunicare nello stesso momento, ci sono due tecniche per gestire gli accessi al mezzo trasmissivo:

- **Distributed Coordination Function (DCF)** - I nodi si contendono l’accesso al canale
- **Point Coordination Function (PCF)** - Non c’è contesa e l’AP coordina l’accesso dei nodi al canale.

Da adesso in poi vedremo in **DCF** che utilizza [[#CSMA/CA (Collision Avoidance)]] per ridurre le collisioni.

## CSMA/CA (Collision Avoidance)

L'obbiettivo è evitare le collisioni, ovvero due o più nodi che trasmettono simultaneamente. Per questo è utilizzato il **carrier sense**, ovvero si ascolta il canale prima di trasmettere.

Non è utilizzato il [[Protocolli del Livello Collegamento#CSMA/CD (collision detection)|CSMA/CD]] (collision detection) per 3 motivi:
- Impossibilità di trasmettere e ricevere nello stesso momento
- [[#^8d9266|Hidden Terminal Problem]]
- Raggio di trasmissione limitato, è quindi difficile ascoltare tutte le trasmissioni

Ci sono diversi metodi per implementare il Collision Avoidance:
- [[#CSMA/CA con ACK]]
- [[#CSMA/CA con Spazio Interframe]]
- [[#CSMA/CA con Finestra di Contesa]]
- [[#CSMA/CA con DIFS + Finestra di Contesa]]
- [[#CSMA/CA con RTS/CTS]]

### CSMA/CA con ACK

IFS (spazio interframe): Rilevata la portante, se il canale risulta libero, si posticipa la trasmissione per evitare che stazioni che hanno già iniziato a trasmettere collidano con la stazione che vuole trasmettere.

![[Pasted image 20250614183736.png|350]]

Il **mittente ascolta** il canale se resta libero per **DIFS tempo** allora trasmette.
- ***DIFS:*** Distributed Interframe Spacing

Il **ricevente** se riceve correttamente il frame allora invia **ACK** dopo **SIFS tempo**.
- ***SIFS***: Short Interframe Spacing

>***DIFS > SIFS*** per dare priorità alle comunicazioni già iniziate (priorità ad ack)

Quindi se durante l’intervallo DIFS il canale diventa occupato allora il nodo interrompe il conteggio DIFS e aspetta che il canale torni completamente libero, quando succede riavvia da zero il conteggio del DIFS completo.
### CSMA/CA con Spazio Interframe

Questa tecnica necessita di un riscontro (ACK) per capire se una trasmissione è andata a buon fine.

![[Pasted image 20250614184316.png|350]]

Viene utilizzato un **doppio carrier sense**: 
- uno sui *dati*
- uno per l'*ACK*

Quando il mittente riceve un ACK capisce che la comunicazione è andata a buon fine. 

Il mittente però non può aspettare l’ACK all’infinito e imposta quindi un timer (ACK timeout), se il timer scade senza aver ricevuto l’ACK allora il nodo suppone che la trasmissione sia fallita e tenta una ritrasmissione.

>***Nota:*** C’è possibilità di collisione anche sugli ACK.

### CSMA/CA con Finestra di Contesa

Dopo aver atteso un tempo IFS, se il canale è ancora inattivo la stazione attente un ulteriore tempo di contesa.

>[!note] Finestra di Contesa (Contention Windows)
>
>La Contention Windows (**CW**) è un lasso di tempo (backoff) per cui deve "sentire" il canale libero prima di trasmettere. Questo tempo è diviso in *slot* e ad ogni slot è eseguito il carrier sense del canale:
>- Si sceglie `R` random in `[0, CW]`.
>- Finché `R > 0` si ascolta il canale per uno slot e se questo è libero per la durata dello slot allora `R - 1` altrimenti si interrompe il timer e aspetta che il canale si liberi e poi si riavvia il timer.
>  
>![[Pasted image 20250614184923.png|700]]

### CSMA/CA con DIFS + Finestra di Contesa

Fase 1: **Attesa dell'IFS (es. DIFS)**:
1. Il nodo rileva il canale libero.
2. Attende un tempo fisso: DIFS (es. 34 μs in IEEE 802.11b).
3. Se il canale rimane libero per tutto il DIFS passa alla finestra di contesa.

Fase 2: **Finestra di contesa (Backoff)**:
1. Il nodo sceglie un numero casuale in un intervallo `[0,CW−1]`, dove CW è la Contention Window.
2. Ogni unità di tempo della finestra si chiama Slot Time (es. 20 μs).
3. Il nodo inizia a contare all’indietro (backoff counter), solo se il canale rimane libero.

>[!example] Esempio
>
>Abbiamo:
>- `CW = 16`, quindi intervallo è `[0,15]`
>
>Supponiamo che il nodo dall'intervallo scelga casualmente `7`, quindi:
>- attende $7 \cdot \text{SoltTime} = 7 \cdot 20\mu s = 140\mu s$, solamente se i canale è libero.
>
>Infatti, se durante questo intervallo un altro nodo inizia a trasmettere, allora il nodo mette in pausa il countdown e, non appena il canale torna libero, riprende dal punto in cui si era interrotto.

### CSMA/CA con RTS/CTS

Il problema dell’hidden terminal non viene risolto né con l’IFS né con la finestra di contesa: è necessario un meccanismo di prenotazione esplicita del canale, ovvero il protocollo RTS/CTS (Request to Send / Clear to Send).

![[Pasted image 20250615115531.png|600]]

Per riservare il canale si utilizza il meccanismo RTS/CTS:

1. Il mittente invia un frame RTS (Request To Send) all’Access Point (o al destinatario).
2. Se il canale è libero, il nodo destinatario risponde con un frame CTS (Clear To Send), trasmesso in broadcast.
3. Tutte le stazioni che ricevono il CTS rimangono a “silenzio” per la durata indicata nel frame, evitando di trasmettere e prevenendo collisioni, anche se si trovano in una posizione “nascosta” rispetto al mittente.
4. Solo il mittente originale, dopo aver ricevuto il CTS, invia i dati.

>[!note] ACK
>Dopo aver trasmesso i dati, il mittente attende un frame ACK dal destinatario. Se l’ACK non arriva entro il timeout previsto, il mittente ritenta la trasmissione del frame.

#### Collisioni sul Destinatario

Come fanno le stazioni che non sono coinvolte nella comunicazione a sapere per quanto tempo devono astenersi dal trasmettere, dato che ascoltando il canale non sono in grado di rilevare la trasmissione?

>[!note] Network Allocation Vector (NAV)
>
>Quando una stazione invia un frame RTS include anche per quanto tempo occuperà il canale per trasmettere il frame e ricevere l’ACK, questo tempo viene incluso anche nel CTS.
>
>Le stazioni influenzate da tale trasmissione avviano un timer chiamato NAV che indica quanto tempo devono attendere prima di eseguire il sensing del segnale. Ogni stazione quindi prima di ascoltare deve controllare sul NAV.

>[!note] Collisioni durante l’handshaking
>
>Una collisione potrebbe accadere anche durante l’invio di RTS o CTS, molto semplicemente se il mittente non riceve un CTS allora assume che c’è stata una collisione e riprova dopo un tempo di backoff.

>[!note] Problema della stazione Esposta
>
>Quando una stazione rinuncia a trasmettere pur avendo il canale libero si parla di “nodo esposto”. Nell’esempio seguente, C è lo stazione esposta:
>
>![[Pasted image 20250615121133.png|700]]
>
>>[!example]- Spiegazione
>>
>>Problema della stazione esposta - Descrizione dei passaggi
>>
>>Contesto:
>>
>>Quattro stazioni wireless: B - A - C - D.
>>
>>- A vuole trasmettere dati a B.
>>
>>- C si trova vicino ad A, ma non può comunicare con B.
>>
>>- C vorrebbe trasmettere a D, ma esita.
>>
>>Passaggi:
>>
>>1. A invia un RTS (Request to Send) a B
>>
>>A chiede a B il permesso di iniziare la trasmissione.
>>
>>Questo messaggio viene ricevuto anche da C, che è nel raggio di A.
>>
>>2. B risponde con un CTS (Clear to Send) ad A
>>
>>B concede ad A il permesso di trasmettere.
>>
>>Il CTS non viene ricevuto da C, perché B è fuori dal suo raggio.
>>
>>3. A inizia la trasmissione dei dati a B
>>
>>Dopo il CTS, A invia i dati a B.
>>
>>4. C riceve l'RTS di A e si astiene dal trasmettere C non sente il CTS e quindi non sa che la comunicazione è diretta tra A e B.
>>
>>Temendo di causare una collisione, C decide di non trasmettere a D, anche se il canale verso D è libero.
>>
>>Problema:
>>- C è una "stazione esposta": sente una richiesta di trasmissione (RTS), ma non è coinvolta nella comunicazione e non interferirebbe, tuttavia decide comunque di non trasmettere, causando un uso inefficiente del canale.

## Formato del Frame

![[Pasted image 20250615122825.png]]

- **Frame Control (FC)** - Tipo del frame e alcune informazioni di controllo
- **D** - Durata della trasmissione, usata per impostare il NAV
- **Indirizzi** - Indirizzi MAC
- **SC** - Informazioni sui frammenti, essenzialmente sono il numero di frammento e di sequenza, servono a distinguere frame ritrasmessi come nel livello di trasporto, questo perché alcuni ACK potrebbero andare perduti.
- **Frame body** - Payload
- **FCS** - Codice CRC a 32 bit

Il **campo FC** è formato quindi da 16 bit, due di questi indicano il tipo, ci sono 3 tipo di frame:

- ***00*** - Frame di Gestione: usati per le comunicazioni iniziali tra stazioni e punti di accesso
- ***01*** - Frame di controllo: Si usano per accedere al canale e dare riscontro, questi usano i successivi 4 bit per informazioni aggiuntive sul tipo:
    - *1011* - RTS
    - *1100* - CTS
    - *1101* - ACK
		- *10* - Frame di dati: Vengono usati per trasportare i dati

>[!note] Frame di controllo
>
>![[Pasted image 20250615123321.png|500]]
## Indirizzamento

![[Pasted image 20250615123439.png|900]]

>***Nota:*** DS sta per sistema di distribuzione.

A seconda del valore di questi due bit (To DS e From DS) i campi degli indirizzi assumono valori diversi:
![[Pasted image 20250615123554.png|800]]

In ordine possiamo visualizzare i casi in questo modo:

![[Pasted image 20250615123615.png|800]]

## Mobilità all’interno della stessa sottorete IP

La mobilità è semplice all’interno della stessa sottorete, infatti l’indirizzo IP rimane lo stesso, ma quando un dispositivo cambio AP come si mantengono attive tutte le connessioni TCP?

Come si comporta lo switch?

- Autoimpara ma non può supportare utenti con elevata mobilità
- AP2 invia un frame broadcast allo switch contenente come indirizzo mittente H1 e lo switch capisce quindi che H1 è nel BSS2