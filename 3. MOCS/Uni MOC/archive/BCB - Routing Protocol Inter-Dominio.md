---
type: Uni Note
class: "[[Reti (class)]]"
academic year: 2024/2025
related:
  - 
completed: false
created: 2025-05-06T14:28
updated: 2025-05-25T23:48
---
## Internet Routing

Come viene eseguito il routing in Internet? Non è possibile utilizzare un solo protocollo di routing. I protocolli visto fino ad ora ([[RIP - Routing Protocol Intra-Domino|RIP]] e [[OSPF - Routing Protocol Intra-Domino|OSPF]]) lavorano su reti di "piccole" dimensioni, composte da router indistinguibili tra di loro (senza gerarchia).

Internet è una rete **gerarchica** composta da più **200 milioni di destinazioni**, utilizzare [[RIP - Routing Protocol Intra-Domino|RIP]] o [[OSPF - Routing Protocol Intra-Domino|OSPF]] in questo caso significherebbe:
- Ogni nodo dovrebbe avere una grandissima quantità di memoria per archiviare le informazioni d’instradamento per ciascuna destinazione.
- Se si utilizza [[OSPF - Routing Protocol Intra-Domino#Algoritmo Link State (LS)|LS]], il traffico dati generato non lascerebbe spazio al traffico dei veri dati da trasmettere.
- [[RIP - Routing Protocol Intra-Domino|DV]] non convergerebbe mai

Inoltre in internet ogni rete è amministrata in modo diverso dal proprio ISP, **autorità amministrativa autonoma**, che utilizza proprie sottoreti come vuole e impone le politiche sul traffico.

## Instradamento Gerarchico

Ogni ISP è un **sistema autonomo (AS)** e quindi può eseguire un qualsiasi protocollo di routing a seconda delle sue esigenze.

>[!note] Protocolli intra-dominio
>
>Ogni router all'interno di uno stesso AS deve eseguire lo stesso protocollo di routing. Il protocollo utilizzato all'interno di un AS è detto:
> - *Protocollo di routing interno al sistema autonomo* (**intra-AS**)
> - *Interior gateway protocol* (**IGP**)
> - *Protocollo intra-dominio*

>[!note] Protocolli inter-dominio
>
>All’esterno degli AS utilizziamo un protocollo che gestisce il routing tra i vari AS, ne deve esistere **uno solo** per tutto l'intranet. Questo protocollo possiamo indicarlo con diversi nomi: 
>- *Protocollo di routing tra sistemi autonomi* (**inter-AS**)
>- *Exterior Gateway Protocol* (**EGP**)
>- *Protocollo inter-dominio*

^34eb10

>[!note] Gateway Router
>
>Il [[#^34eb10|protocollo inter-dominio]] è utilizzato dai *gateway routers*, ovvero quei router che *mettono in connessione due o più AS* e che hanno quindi il compito di inoltrare i pacchetti verso destinazioni esterne.

## Sistemi Autonomi

Ogni ISP è un sistema autonomo, ed ogni AS è identificato da un numero univoco a 16 bit chiamato **Autonomous number (ASN)** assegnato dall’ICANN (Internet Corporation for Assigned Names and Numbers).

Gli AS possono avere *diverse dimensioni* e sono classificati in base al modo in cui sono connessi ad altri AS:
- **AS stub** - ha un solo collegamento verso un altro AS. Il traffico è generato o destinato allo stub ma non transita attraverso di esso. (es. grande azienda)
- **AS multihomed** - ha più di una connessione con altri AS ma non consente transito di traffico. (es. aziende che usano più di un network provider ma non forniscono connettività ad altri AS)
- **AS di transito** - è collegato a più AS e consente il traffico al suo interno. (es. i network provider e le dorsali)

## Instradamento tra sistemi autonomi (inter-AS)

I protocolli [[RIP - Routing Protocol Intra-Domino|RIP]] e [[OSPF - Routing Protocol Intra-Domino|OSPF]] sono utilizzati per determinare i percorsi ottimali per le coppie origine-destinazione interne ad un sistema autonomo.

Per determinare percorsi per coppie origine-destinazione che interessano più sistemi autonomi si utilizza il Border Gateway Protocol **BGP**.

Il BGP è un protocollo di proprietà Cisco che permette di effettuare l'instradamento tra coppie origine-destinazione appartenenti a sistemi autonomi differenti.

>[!note] Path Vector
>
>Questo protocollo utilizza un **path vector** che è simile al *distance vector* ma nel vettore non salviamo le distanze ma i percorsi.
>
>Vedi [[#Patch Vector Routing (PV)]] per saperne di più.

>[!note] Funzionalità
>
>BGP mette a disposizione di ciascun AS un modo per:
>
>- Ottenere informazioni sulla raggiungibilità delle sottoreti da parte di AS confinanti.
>- Propagare le informazioni ricevute a tutti i router interni ad un AS.
>- Determinare percorsi buoni verso le sottoreti sulla base delle informazioni di raggiungibilità e delle politiche dell’AS.
>  
>Più in generale permette ad una sottorete (AS) di comunicare al resto di Internet la sua esistenza.

### Patch Vector Routing (PV)

I protocolli [[OSPF - Routing Protocol Intra-Domino#Algoritmo Link State (LS)|LS]] e [[RIP - Routing Protocol Intra-Domino|DV]] determinano il percorso minimo ma non è sempre l'obbiettivo primario, ad esempio, si potrebbe voler evitare di far transitare i dati su determinati router.

Attraverso il Path-vector routing (routing a vettore di percorso) la sorgente può controllare il percorso, **evitare dei nodi** ed **applicare delle politiche** per la scelta di questo ultimo.

>[!note] Funzionamento
>
>Simile a [[RIP - Routing Protocol Intra-Domino|distance vector (DV)]] ma vengono ***inviati percorsi*** invece che solo destinazioni.
>
>Ogni nodo quando riceve un path vector da un vicino, aggiorna il suo path vector applicando la sua politica (invece del costo minimo).
>
>![[Pasted image 20250520143735.png|650]]
>
>Quindi cosa succede quando `C` riceve una copia del path vector di `B`?
>
>![[Pasted image 20250520143821.png|600]]

## eBGP e iBGP

Ogni router utilizzano una variante del BGP chiamata **BGP interno** o iBGP, inoltre i router di confine (gateway) utilizzano anche il **BGP esterno** o eBGP, quindi:
- I router di confine (gateway) eseguono 3 protocolli di routing: *intra-dominio*, *eBGP*, *iBGP*.
- Mentre gli altri router soltanto due: *iBGP* e *intra-dominio*.

Una **"connessione BGP"** consiste in coppie di router si scambiano le informazioni di instradamento usando TCP sulla porta `179`.
- I router i capi di una connessione TCP prendono il nome di **peer BGP** e la connessione dove avvengono questi scambi di messaggi **sessione BGP**.
- Notiamo che le linee di sessione BGP non sempre corrispondono ai collegamenti fisici.

>[!note] BGP esterno (eBGP)
>
>Due router di confine fisicamente collegati tra loro che si trovano in due AS diversi formano una coppia di peer BGP e si scambiano messaggi.
>
>I messaggi scambiati durante le sessioni eBGP servono per indicare ad alcuni router come instradare i pacchetti destinati an altri AS, ma le informazioni di raggiungibilità non sono complete.
>
>Problemi da risolvere:
>1. I router di confine sanno instradare pacchetti solo ad AS vicini
>2. Nessuno dei router non di confine (interno agli AS) sa come instradare un pacchetto destinato alle reti che si trovano in altri AS
>   
>>***Nota:*** Per risolvere questi problemi si utilizza [[#^dad7e7|iBGP]].
>
>![[Pasted image 20250521081910.png|700]]
>
>As esempio: `R5` sa soltanto instradare ai nodi della sua rete (AS2) ed alla rate del router `R1` (AS1).

>[!note] BGP interno (iBGP)
>
>Una connessione è creata tra ogni possibile coppia di router all’interno di un AS.
>
>In questo dipo di conessione non tutti i nodi hanno messaggi da inviare, ma ogni nodo riceve.
>
>![[Pasted image 20250525234440.png|650]]
>
>l processo di aggiornamento non termina dopo il primo scambio di messaggi, in quest'esempio, `R1` dopo che ha ricevuto il messaggio di aggiornamento di `R2`, combina le informazioni circa la raggiungibilità di `AS3` con quelle che già conosceva relativamente a `AS1` e invia un nuovo messaggio d’aggiornamento a `R5` (che quindi sa come raggiungere AS1 e AS3).

^dad7e7

## Scambio di messaggi

