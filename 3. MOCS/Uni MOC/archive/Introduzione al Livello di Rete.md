---
type: Uni Note
class: "[[Reti (class)]]"
academic year: 2024/2025
related: 
completed: true
created: 2025-05-07T08:04
updated: 2025-05-10T17:11
---
## Introduzione

Il livello di rete si occupa dell’**instradamento dei datagrammi** dal *mittente al destinatario*. A differenza del livello di trasporto che connette due processi, il livello di rete collega due host.

>[!note] Datagrammi
>
>Il livello di rete prende i segmenti del livello di trasporto, e li incapsula trasformandoli in **datagrammi** . Quetsti vengono trasmessi al router più vicino facente parte del percorso.
>
>Il datagramma viene instradato fra i vari router fino a raggiungere l’host destinatario, dove viene decapsulato e inviato al livello di trasporto.

## Funzioni Chiave (routing and forwarding)

Il livello di Rete si occupa di due funzioni principali:
- **Instradamento** (routing): processo che *determina il percorso* seguito dai pacchetti dall’origine alla destinazione.
- **Inoltro** (forwarding): processo che *trasferisce i pacchetti* dall’*input* di un router all’*output* del router appropriato.

Queste operazioni sono rese possibili attraverso:
Tramite gli **algoritmi di routing** vengono create le **tabelle di routing** (o forwarding table), ogni router ne contiene una e specificano quale collegamento di uscita si deve prendere per raggiungere la destinazione dal forwarding.
## Switch e Router

Gli switch e i router sono detti **packet switch (commutatore di pacchetto)** ovvero dei dispositivi che si occupano di trasferire dati da un’*interfaccia di ingresso* ad un *interfaccia di uscita* in base ai valori presenti nei datagrammi.

**Link-layer switch** (commutatore a livello di collegamento) - Stabiliscono il percorso in base al campo presente nell’intestazione a [[Introduzione Livello Collegamento|livello di collegamento]] (livello 2). È principalmente utilizzato per collegare singoli computer all’interno di una LAN

**[[#Router]]** - Stabiliscono il percorso in base al campo presente nell’intestazione a [[Introduzione al Livello di Rete|livello di rete]] (livello 3). Riceve un insieme di informazioni (pacchetto) e in base alle tabelle di routing decide quale sarà il prossimo router su cui instradarlo.

![[Pasted image 20250508115309.png|650]]

## Circuit switching vs. Packet switching

- **Circuit Switching** ([[#Reti a circuito virtuale|rete a circuito virtuale]]) - È un servizio orientato alla connessione, infatti prima che i datagrammi fluiscano, è necessario che i due sistemi terminali e i router intermedi stabiliscono una connessione virtuale.
- **Packet Switching** ([[#Reti a Datagramma|rete a datagramma]]) - Non è orientato alla connessione infatti ogni datagramma viaggia in modo indipendente dagli altri.

### Reti a circuito virtuale

In questo tipo di rete viene quindi stabilita una connessione virtuale che determina il percorso che tutti i pacchetti dovranno seguire.

I pacchetti in un circuito virtuale hanno un’**etichetta di circuito** (***VC***) nella loro intestazione, i router scelgono dove instradare il pacchetto in base a questa etichetta. 

>***Nota:***  VC può essere diverso da router a router, anche riferendosi allo stesso percorso. Per questo durante il passaggio in un router, ad ogni pacchetto, viene cambiato il VC.

![[Pasted image 20250508120425.png|700]]

>[!note] Implementazione
>
>Un circuito virtuale consiste in:
>1. un percorso tra gli host origine e destinazione
>2. numeri VC, uno per ciascun collegamento
>3. righe nella tabella d’inoltro in ciascun router
>
>Il numero di VC rappresenta un etichetta di flusso e cambia su tutti i collegamenti del percorso. I nuovi VC sono rilevati dalla tabella d’inoltro.
>
>![[Pasted image 20250508120721.png|420]]
>
>![[Pasted image 20250508120854.png|700]]
>
>I router mantengono le informazioni sullo stato delle connessioni nella tabella di inoltro:
>- una nuova riga è aggiunta ogni volta che stabiliscono una nuova connessione
>- una riga è rimossa quando la connessione ad essa associata viene rilasciata

>[!note] ATM (Asynchronous transfer mode)
> 
> È una rete orientata alla connessione progettata negli anni 90 con scopo di unificare dati, voce, televisione via cavo. Ad oggi è ancora utilizzata per spostare pacchetti IP all’interno della rete telefonica. 
> 
> Le connessioni vengono chiamate circuiti virtuali (in analogia con quelli telefonici che sono circuiti fisici), una volta stabilita una connessione, entrambe le parti possono trasmettere.

### Reti a Datagramma

***Internet*** è una **rete a datagramma** (packet switched), In questo caso non esiste in concetto di connessione i pacchetti vengono semplicemente inoltrati in altri router in base al loro indirizzo di destinazione.

Questo implica che i pacchetti, aventi la stessa origine e destinazione, potrebbero non seguire più lo stesso percorso.

>[!note] Tabelle di inoltro
>
>Le tabelle di inoltro contenute nei router delle reti a datagramma, non associano ad ogni indirizzo un interfacci d'uscita, questo perché le tabelle sarebbero tropo grandi per coprisse tutte le possibilità.
>
>Per scegliere il percorso viene utilizzato quindi il prefisso degli indirizzi, è come dire che ad ogni interfaccia d'uscita si associa un rage di indirizzi:
>
>![[Pasted image 20250508124955.png|900]]

^e2e187

## Router

Come abbiamo già visto i router si occupano di instradare (routing) i pacchetti e per fare ciò hanno bisogni di implementare soltanto 3 livelli dello [[Introduzione allo stack protocollare TCP-IP|stack protocollare TCP-IP]]:
- **Fisico**
- **Collegamento**
- **Rete**

La loro strutta interna è composta da:

- **[[#Porte di ingresso|Porte (interfacce) di ingresso]]**
- **[[#Table Lookup|Processore di routing]]** - implementa il livello di rete, ed in particolare esegue table lookup delle tabelle di routing.
- **[[#Tecniche Commutazione|Switch fabric]]** - struttura di commutazione che fisicamente sposta i datagrammi dalla coda di input alla coda di output.
- **[[#Porte di uscita|Porte (interfacce) di uscita]]**

![[Pasted image 20250508130221.png|700]]

### Porte di ingresso

Le porte di ingresso lavora sia sul livello fisico che il livello di collegamento (a volte anche rete) infatti sono composte da:
- ***Line termination*** (livello fisico) che riceve i bit.
- ***Data link processing*** (livello collegamento) che effettua il decapsulamento dei pacchetti trasformandoli in datagrammi.

A volte le porte in ingresso possono anche lavorare sul livello di rete implementando il processo di [[#Table Lookup]] utilizzando la [[#^e60995|commutazione decentralizata]].

![[Pasted image 20250508142937.png|700]]

>[!note] Commutazione Decentralizzata
>
>La [[#Tecniche Commutazione|commutazione]] può avvenire anche direttamente sulle porte, prende il nome di **commutazione decentralizzata**, questa è permessa da una copia della tabella d’inoltro nella porta di ingresso.
>
>Effettuare la commutazione diretta in ingresso ha l'obbiettivo di elaborare gli input nello stesso memento in cui arrivano, in modo tale da non creare colli di bottiglia.
>
>Una volta determinata la porta di uscita il pacchetto verrà inoltrato alla struttura di commutazione.

^e60995

### Table Lookup

Processo che consiste nel determinare la porte di uscita di un determinato datagramma in ingresso, per fare ciò si deve cercare nella [[#^e2e187|tabella di inoltro]] la porta di uscita associata all'indirizzo di destinazione del datagramma in ingresso.

Per assicurare che questa ricerca sia fatta velocemente, le tabelle hanno una **struttura ad albero**:
- Ogni *livello* dell’albero corrisponde a un *bit* dell’*indirizzo* di destinazione
- Per cercare un indirizzo si comincia dalla radice dell’albero
	- Se 0 allora sottoalbero di sinistra
	- Se 1 allora sottoalbero di destra

Quindi la ricerca richiede `n` passi dove `n` è il numero di bit nell’indirizzo.

### Tecniche Commutazione

Esistono 3 principali modi per effettuare la commutazione dei pacchetti:
- [[#^a1847a|Commutazione in Memoria]]
- [[#^a6a770|Commutazione tramite bus]]
- [[#^6e26b7|Commutazione attraverso rete d’interconnessione (crossbar)]]

![[Pasted image 20250508145122.png|900]]

>[!note] Commutazione in Memoria
>
>Utilizzata dalle *prime generazioni di router*, dove la commutazione era effettuata sotto il *controllo diretto della CPU*.
>
>Il pacchetto veniva copiato nella memoria del processore e poi trasferito nelle porte di output.

^a1847a

>[!note] Commutazione tramite bus
>
>Le porte di ingresso *trasferiscono* i pacchetti direttamente alle porte di output *tramite un bus condiviso* (disegno sopra).
>
>In questo modo però si può **trasferire un solo pacchetto alla volta**, inoltre la *larghezza di banda* della commutazione è *limitata* da quella del bus. I pacchetti in ingresso che trovano il bus occupato vengono allocati in una coda.
>
>>Alcuni router però hanno bus da 32Gbps che sono sufficienti per reti d’accesso o aziendali.

^a6a770

>[!note] Commutazione attraverso rete d’interconnessione (crossbar)
>
>Tecnica che permette di superare il limite di larghezza di banda di un solo bus.
>
>Si usa una **crossbar switch** ovvero una rete che consiste di `2n` bus che collegano `n` porte d’ingresso a `n` porte d’uscita (disegno sopra). 
>
>Attualmente si utilizza questa rete frammentando i pacchetti in celle di dimensione fissa, poi verranno diassemblati alla porta d’uscita.
>
>>I router di oggi utilizzano reti d’interconnessione fino a 60Gbps

^6e26b7
### Porte di uscita

Le porte di uscita effettuano il processo inverso rispetto alle [[#Protocolli a livello di Rete|porte di ingresso]].

**Funzionalità di accodamento** - utilizzate quando struttura di commutazione consegna pacchetti alla porta d’uscita a una frequenza che supera quella del collegamento uscente.

**Schedatore di pacchetti** - stabilisce in quale ordine trasmettere i pacchetti 

![[Pasted image 20250508151338.png|700]]

### Funzionamento dell'accodamento

L'accodamento si utilizza sia nelle porte di ingresso che nelle porte di uscita.

>[!note] Accodamento su porte di ingresso
>
>Avviene quando:
>- la velocità di commutazione è inferiore alla frequenza dei pacchetti in ingresso.
>- avviene un blocco in testa alla fila (HOL: head-of-the-line blocking) ovvero quando un pacchetto nella coda d’ingresso deve attendere il suo trasferimento, anche se la sua coda è libera, perché in testa alla coda c’è un pacchetto bloccato.
>  
>![[Pasted image 20250508152403.png|600]]
>  
>Il pacchetto verde potrebbe passare ma è bloccato da quello rosso.
>
>>***Perdita di dati:*** se le sono saturare i pacchetti in eccesso vengono scartati.  

>[!note] Accodamento sulle porte di uscita
>
>Avviene quando:
>- Velocità di commutazione superiore a quello di uscita
>- Troppi pacchetti sulla stessa uscita
>
>>***Perdita di dati:*** se le si saturano i pacchetti in eccesso vengono scartati.

>[!question] Che capacità dovrebbero avere?
>
>Per diversi anni si è seguira la regola definita in RFC 3439, ovvero una media del tempo di andata e ritorno per la capacità del collegamento.
>
>*Ad esempio:* se abbiamo un RTT di 250ms e il collegamento `C` da 10Gbps avremo buffer da 2.5Gbit.
>
>Attuali raccomandazioni dicono che la quantità di buffering necessaria per `N` flussi TCP con capacita di collegamento `C` è:
>
>$$
> \frac{RTT \cdot  C}{\sqrt{ N }}
>$$
## Protocolli a livello di Rete

A livello di rete ci sono diversi protocolli di cui alcuni dei più importanti ed utilizzati sono:
- IP: Internet Protocol [[Internet Protocol v4 (IPv4) - Indirizzamento, DHCP, NAT, Forwarding|v4]] e [[Internet Protocol v4 (IPv4) - Indirizzamento, DHCP, NAT, Forwarding|v6]]
- IGMP: Internet Group Management Protocol (multicasting)
- [[Internet Control Message Protocol (ICMP)|ICMP]]: Internet Control Message Protocol (gestione errori)
- ARP: Address Resolution Protocol (associazione indirizzo IP – ind. collegamento)
+ Protocolli di Routing