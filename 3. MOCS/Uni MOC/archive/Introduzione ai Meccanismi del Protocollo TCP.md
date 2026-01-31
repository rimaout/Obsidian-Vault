---
type: Uni Note
class: "[[Reti (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-04-09T17:42
updated: 2026-01-31T13:32
---
## Introduzione

Il protocollo TCP è un servizio **affidabile** ed [[#Servizio Connection Oriented|orientato alla connessione]], per questo è richiesto un setup fra i processi *client* e *server*.

>[!note] Servizi Forniti
>Stesse cose fornite dal [[Protocollo UDP (User Datagram Protocol)|UDP]]:
>- Comunicazione tra processi utilizzando i [[Introduzione Livello Trasporto#Socket|Socket]]
>- [[Introduzione Livello Trasporto#Incapsulamento e Decapsulamento|Multiplexing/demultiplexing]] dei pacchetti
>- [[Introduzione Livello Trasporto#Incapsulamento e Decapsulamento|Incapsulamento e decapsulamento]]
>  
>Inoltre fornisce funzionalità avanzate come:
>- **Trasporto affidabile** fra i processi di invianti e riceventi.
>- **Controllo di flusso:** il mittente cerca di non sovraccaricare il destinatario
>- **Controllo della congestione:** Riduce i dati inviati quando le rete è sovraccaricata

>[!note] Servizi non Forniti
>
>Non fornisce temporizzazione, garanzie su un ampiezza di banda minima, sicurezza (alcune possono essere implementate, es. SSL)

>[!warning] Flusso di Byte
>
 >Una delle differenze con il protocollo UDP è che la comunicazione tra mittente e ricevente può essere vista come un flusso di byte e non come un invio di pacchetti.
 >
 >![[Pasted image 20250409180026.png|1000]]

## Servizio Connection Oriented

Il TCP è un servizio orientato alla concessione, per questo prima del inizio dell'invio dei dati veri e propri i due terminali devono stabilire una connessione logica.

Questo permette ai due terminali di avere delle comunicazioni bilaterali rendendo possibile implementare:
- [[#Controllo Flusso|Controllo di flusso]]
- [[#Controllo Errori|Controllo degli errori]]
- [[#Controllo Congestione|Controllo della congestione]]

>[!note] Rappresentazione mediante Finite State Machine
>
>![[Screenshot 2025-04-10 at 09.23.08.png|700]]

## Demultiplexing (orientato alla connessione)

La socket TCP è identificata da 4 parametri:
- *Indirizzo IP* e *porta di origine*
- *Indirizzo IP* e *porta di destinazione*

Un host server può supportare più socket TCP contemporanee dato che ogni socket è identificata dai 4 parametri. Si avrà una socket differente anche per lo stesso client, ogni richiesta viene trasmessa su una diversa socket.

Essenzialmente il server accetta tutte le connessioni sulla stessa socket e poi le sposta su una porta differente.

![[Pasted image 20250409180957.png|800]]

## Controllo Flusso

Quando un’entità produce dati che un’altra entità deve consumare, deve esistere un **equilibrio fra la velocità di produzione e la velocità di consumo** dei dati.

- Se `velocità di produzione > velocità di consumo` - il consumatore potrebbe essere **sovraccaricato** e costretto a eliminarne alcuni dati in input
- Se `velocità di produzione < velocità di consumo` -  l consumatore rimane in attesa **riducendo l’efficienza** del sistema

La soluzione consiste nel utilizzare dei buffer, ovvero zone di memoria che memorizzano pacchetti, questo permette al consumatore (ricevente) di notificare il produttore (mittente) quando il suo buffer è saturo in modo tale da ridurre la produzione ed evitare perdita di dati.

Come vedremo l'utilizzo di un buffer, permetterà al consumatore anche di dati che arrivano in un ordine sbagliato.

>[!note] Entità
>
>![[Screenshot 2025-04-10 at 09.38.45.png|850]]
>
>Il sistema è composto da 4 **entità**:
>- processo mittente
>- trasporto mittente
>- trasporto destinatario
>- processo destinatario
>  
>E abbia due casi di **controllo di flusso**:
>- processo mittente -> trasporto mittente
>- trasporto destinatario -> processo destinatario
>  
>
>Il **livello trasporto del mittente** segnala al **livello applicazione** di sospendere l’invio di messaggi quando ha il buffer saturo, quando si libera spazio nel buffer segnala al livello applicazione che può riprendere l’invio di messaggi.
>
>Il **livello trasporto del destinatario** segnala al **livello trasporto del mittente** di sospendere l’invio di messaggi quando ha il buffer saturo, quando si libera spazio nel buffer segnala al livello trasporto mittente che può riprendere l’invio di messaggi.

## Controllo Errori

Dato che il livello di rete è inaffidabile, l’affidabilità va implementata a livello di trasporto e per farlo abbiamo bisogno di implementare un controllo degli errori che agisce sui pacchetti:

- Rilevare e scartare pacchetti corrotti
- Tracciare i pacchetti persi e il loro rinvio
- Riconoscere pacchetti duplicati
- Bufferizzare i pacchetti fuori sequenza finché non arrivano quelli mancanti

È il livello trasporto del destinatario a gestire il controllo errori e segnalarli al livello trasporto mittente.

>[!note] Realizzazione
>
>I pacchetti vengono numerati in modo sequenziale attraverso un campo nell’header.
>
>Poiché il numero di sequenza va inserito nell’intestazione, va specificata la dimensione massima:
>
>- Se l’intestazione prevede `m` bit per il numero di sequenza questi possono assumere valori da $0$ a $2^{m}-1$
>- I numeri di sequenza sono quindi considerati in modulo $2^{m}$ (ciclici)
>
>Questo numero di sequenza serve al destinatario per:
>
>- Capire la ordine dei pacchetti in arrivo
>- Se ci sono pacchetti persi
>- Se ci sono pacchetti duplicati
>
>Ma il mittente come fa a capire che un pacchetto è andato perso?
>
>- Il destinatario ad un ogni pacchetto ricevuto invia un **ACK (acknowledgment)** con il numero del pacchetto che ha ricevuto che funziona da notifica di ricezione.

### Integrazione del controllo degli errori e controllo di flusso

Precedentemente abbiamo visto che:
- Il controllo del flusso richiede 2 buffer uno per il mittente e uno per il destinatario
- Il controllo degli errori richiede un numero di sequenza e dei messaggi ACK

É possibile combinare i due meccanismi tramite dei buffer numerati nel mittente e nel destinatario.

Il **mittente**:
- Quando prepara un pacchetto usa come come numero di sequenza il numero (`x`)
- Quando invia il pacchetto ne memorizza una copia nella locazione `x` del buffer
- Quando riceve il segnale ACK di un pacchetto libera la posizione di memoria occupata da quel pacchetto

Il **destinatario**:
- Quando riceve un pacchetto con numero `y` lo memorizza nella locazione `y` fino a quando il livello applicazione non è pronto a riceverlo
- Quando passa il pacchetto al livello applicazione invia ACK al mittente

>[!note] Sliding Window
>
>Dato che i numeri di sequenza sono calcolati in modulo $2^{m}$ e quindi ciclici possiamo rappresentarli tramite un cerchio. Il buffer viene rappresentato con un insieme di settori chiamati **sliding windows** che occupano una parte del cerchio.
>
>![[Screenshot 2025-04-10 at 11.03.16.png|800]]
>
>Quindi finché il destinatario non svuota il suo buffer non vengono inviati nuovi pacchetti in modo da non sovraccaricare la rete.
>
>Nella realtà per memorizzare i numeri di sequenza del prossimo pacchetto da inviare e dell’ultimo inviato si usano delle variabili e le sliding windows vengono rappresentate in modo lineare:
>
>![[Pasted image 20250410110758.png|800]]
## Controllo Congestione

Nella commutazione a pacchetto la congestione avviene se il carico della rete, ovvero il numero di pacchetti su di essa, è superiore alla sua capacità, con il controllo della congestione usiamo delle tecniche per fare in modo che questa situazione non si verifichi mai.

Si parla di congestione perché arrivano più pacchetti di quelli che router e switch riescono a gestire e quindi si riempiono le loro code portando alla perdita di pacchetti e rallentamenti.

## Meccanismi 

In questa lezione vediamo meccanismi (non protocolli) per implementare i controlli visti precedentemente:
- [[#Stop and Wait]]
- [[#Go back N]]
- [[#Selective Repeat]]

## Stop and Wait

In questo meccanismo sia il mittente che il destinatario hanno una finestra scorrevole di *un solo pacchetto* e permette di garantire:

- **Controllo errori**: Tramite il *numero di sequenza* dei pacchetti, l’ACK e Timer
- **Controllo del flusso**: Non è possibile inviare più di un pacchetto quindi non possono arrivare in ordine sparso.

>[!note] Funzionamento
>
>1. Il **mittente** *invia* un pacchetto e attende il suo ACK prima di inviarne un'altro.
>2. Quando il pacchetto arriva, il **destinatario** calcola il suo *checksum* se:
>	- Pacchetto non è corrotto --> invio ack al mittente
>	- Pacchetto corrotto --> scartato senza informare il mittente
>1. Il mittente capisce che il pacchetto non è stato ricevuto correttamente tramite un timer:
>	- Scadenza timer senza ricevere ack --> rinvio pacchetto
>
>Questo significa che il **mittente** deve tenere una **copia** del pacchetto fino a che non riceve il suo ACK.

>[!note] Gestione Duplicati
>
>Per gestire i pacchetti duplicati lo stop and wait utilizza i **numeri di sequenza**, in questo caso bastano due valori `0` e `1`.
>
>Quando viene ricevuto un pacchetto si invia un ACK con il numero di sequenza successivo, quindi se ricevo 0 invio ACK 1 e se ricevo 1 invio ACK 0, questo sta ad indicare qualche pacchetto sta aspettando.

>[!note] FSM (finite state machine)
>
>![[Pasted image 20250412115232.png|700]]
>
>Quindi il mittente invia un pacchetto e aspetta un riscontro o la fine del timer prima di inviarne un altro.
>
>![[Pasted image 20250412115238.png|700]]
>
>Quindi il destinatario è sempre pronto a ricevere pacchetti e non va mai in stato di blocked.

>[!note] (In)efficenza
>
>Questo meccanismo può essere particolarmente inefficiente quando abbiamo un *rate elevato* e *ritardo consistente*.
>
>Prendiamo ad esempio un sistema che ha:
>
>- Rate = `1Mbps`
>- Ritardo di andata e ritorno di 1 bit = `20 ms`
>
>Abbiamo un valore di `rate * ritardo = 20'000 bit/ms`
>
>I pacchetti hanno dimensione `1000bit` quindi significa che l’utilizzo del canale è `1000 / 20000 = 5%` dato che possiamo inviare un solo pacchetto alla volta. Abbiamo quindi una rete molto inefficiente.
>
>>**Soluzione:** utilizziamo **protocolli con pipeline**, ovvero dove il mittente può inviare più di un pacchetto alla volta. Vediamo [[#Go back N]] e [[#Ripetizione selettiva]]
>
>>***oss:*** modulo $2^{1}$

## Go back N

In questo meccanismo i numeri di sequenza sono calcolati modulo $2^{m}$ dove $m$ è la dimensione del numero di sequenza in bit.

Anche con questo meccanismo gli ACK inviati contengono il numero che stiamo aspettando, la differenza è che qui usiamo un **ACK cumulativo** ovvero tutti i pacchetti fino al numero di sequenza indicato nell’ACK sono stati ricevuti correttamente.

Quindi se `ACK = 7` significa che tutti pacchetti ricevuti con numero di sequenza minore uguale (`<=`) a `6` sono stati ricevuti correttamente e che si sta spettando il pacchetto `7`.

>[!note] Finestra di Invio
>
>La finestra di invio è un concetto astratto che definisce una porzione immaginaria di dimensione massima $2^{m}-1$ con tre variabili $S_{f}$, $S_{n}$, $S_{\text{size}}$.
>
>![[Pasted image 20250412155747.png|850]]
>
>La finestra di invio può scorrere uno o più posizioni quando viene ricevuto un riscontro privo di errori con ack non maggiore o uguale a $S_{f}$ e, minore di $S_{n}$ in aritmetica modulare.
>
>>[!example]- Esempio
>>
>>![[Pasted image 20250412160816.png|600]]
>>
>>Quindi se ad esempio arriva un ACK = 6
>>
>>![[Pasted image 20250412160846.png|600]]

>[!note] Finestra di Ricezione
>
>La finestra di ricezione ha dimensione `1` per questo il destinatario è sempre in attesa di uno specifico pacchetto, e qualsiasi pacchetto arrivato fuori sequenza viene scartato.
>
>![[Pasted image 20250412162842.png|600]]
>
>***Esempio:*** siamo in attesa di 5 ed arrivano 6 e 7 questi verranno scartati e dovranno essere rinviati successivamente.

>[!note] Timer e Rispedizione
>
>Il **mittente** mantiene un timer per il più vecchio pacchetto non riscontrato dove allo scadere del timer vengono rispediti tutti i pacchetti in attesa di riscontro (il destinatario ha finestra di ricezione pari a 1 e non può memorizzare i pacchetti fuori sequenza).
>
>>***Esempio:*** `Sf = 3` e il mittente ha inviato il pacchetto `6` (`Sn = 7`). Scade il timer, allora i pacchetti `3`, `4`, `5`, `6` non sono stati riscontrati e devono essere rispediti.

>[!note] FSM (finite state machine)
>
>![[Pasted image 20250412164139.png|650]]
>
>In questo esempio gli ACK non vengono mai ricevuti dal mittente, 
>
>![[Pasted image 20250412164144.png|650]]

>[!example]- Esempio Funzionamento
>
>![[Screenshot 2025-04-14 at 10.47.34.png|800]]

>[!warning] Perché Finestra di Invio < 2^m
>
>La finestra di invio deve essere sempre minore di di $2^{m}$, infatti se la finestra di scorrimento fosse troppo grande, il ricevitore potrebbe ricevere un pacchetto con un numero di sequenza che è già stato utilizzato in precedenza, ma che non è ancora stato confermato (ACK).
>
>>[!example]- Esempio
>>
>>![[Pasted image 20250414145821.png|800]]
>>
>>![[Pasted image 20250414150719.png|600]]

## Selective Repeat

Come abbiamo visto, nel meccanismo [[#Go back N]] quando un pacchetto non è ricevuto correttamente tutti i pacchetti presenti nella finestra vengono rinviati, e questo può portare a due problematiche:
1. Non è efficiente rispedire cose che abbiamo erano già state spedite correttamente
2. Se il motivo della non corretta ricezione dei pacchetti è dovuto ad una congestione della rete allora questo meccanismo va ad ulteriormente sovraccaricare il sistema.

Questi problemi sono risolti del meccanismo **selective repeat** (ripetizione selettiva), che permette di rispedire soltanto i pacchetti per i quali non è stato ricevuto un ACK.

>[!note] Funzionamento
>
>In questo meccanismo abbiamo che la **finestra di invio e ricezione** hanno la **stessa dimensione**.
>
>In particolare non deve superare $2^{m-1}$, leggi [[#^32435467|approfondimento dimensioni finestre]] per capire il perché.
>
>Il **mittente** mantiene un timer specifico per ogni pacchetto inviato di cui non ha ancora ricevuto l'ACK e li rinvia se il timer scade.
>
>Il **ricevente** invia un ACK specifico per ogni pacchetto che riceve correttamente e può anche memorizzare i pacchetti fuori sequenza.
>
>![[Pasted image 20250414153241.png|800]]
>
>>***oss:*** se `ACK = 7` non significa più che stiamo aspettando il 7 e abbiamo ricevuto il 6 ma significa che abbiamo ricevuto correttamente il 7.

>[!note] Finite State Machine
>
>![[Pasted image 20250414154252.png|800]]
>
>![[Pasted image 20250414154335.png|800]]

>[!warning] Approfondimento dimensione finestre
>
>Le dimensione delle finestre abbiamo detto essere uguali e in questo meccanismo sono calcolate modulo $2^{m-1}$.
>
>Perché non possiamo usare $2^{m-1}$?
>
>![[Pasted image 20250414155501.png|500]]
>
>In questo caso scade il timer per `0` e viene rispedito, il destinatario lo prende come nuovo pacchetto ma in realtà è un duplicato.
>
>Se usiamo $2^{m}-1$:
>
>![[Pasted image 20250414155356.png|600]]

^32435467

## Altro

>[!note] Protocolli Bidirezionali: Piggybacking
> 
> I meccanismi che abbiamo visto li abbiamo presentati in modo unidirezionale ovvero i pacchetti vengono spediti in una direzione e gli ACK in un’altra ma in realtà questi viaggiano in entrambe le direzioni, sia pacchetti che ACK. Per migliorare l’efficienza dei protocolli bidirezionali si usa la tecnica **piggybacking** ovvero quando un pacchetto trasporta dati da A a B può trasportare anche gli ACK relativi ai pacchetti ricevuti da B e viceversa.

![[Pasted image 20250414161111.png|800]]

