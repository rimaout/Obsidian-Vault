---
type: Uni Note
class: "[[Reti (class)]]"
academic year: 2024/2025
related: 
completed: true
created: 2025-05-06T14:28
updated: 2025-06-15T18:29
---
## Internet Routing

Come viene eseguito il routing in Internet? Non è possibile utilizzare un solo protocollo di routing. I protocolli visto fino ad ora ([[RIP e DV - Routing Protocol Intra-Domino|RIP]] e [[OSPF e LS - Routing Protocol Intra-Domino|OSPF]]) lavorano su reti di "piccole" dimensioni, composte da router indistinguibili tra di loro (senza gerarchia).

Internet è una rete **gerarchica** composta da più **200 milioni di destinazioni**, utilizzare [[RIP e DV - Routing Protocol Intra-Domino|RIP]] o [[OSPF e LS - Routing Protocol Intra-Domino|OSPF]] in questo caso significherebbe:
- Ogni nodo dovrebbe avere una grandissima quantità di memoria per archiviare le informazioni d’instradamento per ciascuna destinazione.
- Se si utilizza [[OSPF e LS - Routing Protocol Intra-Domino#Algoritmo Link State (LS)|LS]], il traffico dati generato non lascerebbe spazio al traffico dei veri dati da trasmettere.
- [[RIP e DV - Routing Protocol Intra-Domino|DV]] non convergerebbe mai

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
- **AS stub** - ha un solo collegamento verso un altro AS. Il traffico è generato o destinato allo stub ma non transita attraverso di esso (es. grande azienda). ^dcda86
- **AS multihomed** - ha più di una connessione con altri AS ma non consente transito di traffico (es. aziende che usano più di un network provider ma non forniscono connettività ad altri AS). ^d78acf
- **AS di transito** - è collegato a più AS e consente il traffico al suo interno (es. i network provider e le dorsali). ^45a215

## Instradamento tra sistemi autonomi (inter-AS)

I protocolli [[RIP e DV - Routing Protocol Intra-Domino|RIP]] e [[OSPF e LS - Routing Protocol Intra-Domino|OSPF]] sono utilizzati per determinare i percorsi ottimali per le coppie origine-destinazione interne ad un sistema autonomo.

Per determinare percorsi per coppie origine-destinazione che interessano più sistemi autonomi si utilizza il Border Gateway Protocol **BGP**.

Il BGP è un protocollo di proprietà Cisco che permette di effettuare l'instradamento tra coppie origine-destinazione appartenenti a sistemi autonomi differenti.

>[!note] Path Vector
>
>Questo protocollo utilizza un **path vector** che è simile al *distance vector* ma nel vettore non salviamo le distanze ma i percorsi.
>
>Vedi [[#Path Vector Routing (PV)]] per saperne di più.

>[!note] Funzionalità
>
>BGP mette a disposizione di ciascun AS un modo per:
>
>- Ottenere informazioni sulla raggiungibilità delle sottoreti da parte di AS confinanti.
>- Propagare le informazioni ricevute a tutti i router interni ad un AS.
>- Determinare percorsi buoni verso le sottoreti sulla base delle informazioni di raggiungibilità e delle politiche dell’AS.
>  
>Più in generale permette ad una sottorete (AS) di comunicare al resto di Internet la sua esistenza.

### Path Vector Routing (PV)

I protocolli [[OSPF e LS - Routing Protocol Intra-Domino#Algoritmo Link State (LS)|LS]] e [[RIP e DV - Routing Protocol Intra-Domino|DV]] determinano il percorso minimo ma non è sempre l'obbiettivo primario, ad esempio, si potrebbe voler evitare di far transitare i dati su determinati router.

Attraverso il Path-vector routing (routing a vettore di percorso) la sorgente può controllare il percorso, **evitare dei nodi** ed **applicare delle politiche** per la scelta di questo ultimo.

>[!note] Funzionamento
>
>Simile a [[RIP e DV - Routing Protocol Intra-Domino|distance vector (DV)]] ma vengono ***inviati percorsi*** invece che solo destinazioni.
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

## Tabelle di Percorso

Dopo lo scambio di messaggi avvenuti in [[#eBGP e iBGP]], ogni router crea la propria tabella di percorso.

Le tabelle di percorso contengono una riga per ogni AS (escluso l'AS del router che ha creato la tabella), con le seguenti informazioni:

- Il _percorso_ rappresenta gli AS in cui si passa per raggiungere la rete, dove l'ultimo indica l'AS da raggiungere.
- Il _prossimo router_ rappresenta il router addicente in cui si passa per raggiungere la rete
- La _rete_ indica i nodi raggiungibili.

Le tabelle di percorso ottenute da BGP non vengono usate di per sé per l’instradamento dei pacchetti bensì inserite nelle [[#Tabelle di Routing|tabelle di routing]] intra-dominio ([[RIP e DV - Routing Protocol Intra-Domino|RIP]] o [[OSPF e LS - Routing Protocol Intra-Domino|OSPF]]).

>[!note] Esempio
>
>Esempio di tabelle di percorso generate dai nodi dell'[[#eBGP e iBGP|esempio precedente]]:
>
>![[Pasted image 20250602113849.png|800]]
>
>![[Pasted image 20250605171823.png|800]]

## Tabelle di Routing

La struttura delle tabelle di routing cambia in base se si trova in un router appartenete ad uno [[#^d6abab|AS stub]] o ad un [[#^98bc36|AS di transito]].

In generale ogni riga è composta da tre elementi:
- ***Des*** ovvero la destinazione da raggiungere
- ***Pross*** ovvero il prossimo router adiacente a cui inoltrare il pacchetto che ha come destinazione *des*, se il nodo destinazione è adiacente al router non si scrive niente.
- ***Costo*** ovvero **NON HO CAPITO COME SI DETERMINA IL COSTO**

>[!note] Tabella Routing (AS Stub)
>
>Ricordiamo che un [[#^dcda86|AS stub]] è un sistema autonomo che ha un solo collegamento verso l'esterno.
>
>Quando il router fa parte di uno AS stub, la sua tabella di routing contiene una riga per ogni nodo della AS.
>
>Inoltre alla fine della tabella è presente una riga che indica indica come "raggiungere il mondo esterno", in particolare, se il router è:
>- **Router di Confine** (gateway) allora contiene come prossimo router quello che si trova dall’altro lato della connessione eBGP (destinazione 0).
>- **Router Intermedio** allora contiene come prossimo router il router di getaway (destinazione 0).
>  
>  Ad esempio:
>  ![[Pasted image 20250605172726.png|900]]

^d6abab

>[!note] Tabella Routing (AS di Transito)
>
>Ricordiamo che un [[#^45a215|AS di transito]] è un sistema autonomo che è collegato collegato a più sistemi autonomi e permette il transito di traffico al suo interno.
>
>Quando il router fa parte di uno AS di transito, la sua tabella di routing contiene una riga per ogni nodo della AS.
>
>Inoltre alla fine della tabella di routing inseriamo tutte le righe che possono essere derivate dalla sua tabella di percorso, ma dove sono aggiunti i costi.
>
>>*Ad esempio:*
>>![[Pasted image 20250605175906.png|800]]
>
>![[Pasted image 20250607112702.png|800]]

^98bc36

## Attributi del percorso BGP

Quando un router annuncia una rotta per una *rete (prefisso)* per una sessione BGP, vengono anche inclusi degli **attributi BGP**.

>[!note] Rotta BGP
>
>Una rotta in una sessione BGP non è altro che le combinazione di:
>- un *prefisso* che indica la rete di destinazione
>- un insieme di *attributi BGP*

Due dei più importanti attributi sono:

>[!note] AS-PATH
>
>Serve per la selezione dei percorsi, infatti elenca tutti gli AS attraverso i quali è passato l’annuncio del prefisso ovvero i futuri gli hop intermedi della rotta.
>
>Tutti gli AS, ad eccezione degli stub, hanno un identificativo univoco, gli stub sono evitati in modo da non avere cicli.

^113d2b

>[!note] NEXT-HOP
>
>Indica l’indirizzo IP dell’interfaccia su cui è inviato il pacchetto, ricordiamo infatti che un router ha più indirizzi IP, uno per ogni interfaccia.

Quando un router gateway riceve un annuncio di rotta, utilizzando le sue **politiche di importazione** per decide se accettare o filtrare la rotta, ad esempio:
- L’AS può non voler inviare traffico in qualche AS presente in [[#^113d2b|AS-PATH]].
- Il router conosce una rotta migliore di quella ricevuta.

### Selezione della Rotta

Un router può ricavare più di una rotta verso una destinazione (percorsi multipli), e deve quindi sceglierne una, utilizzando delle **regole di eliminazione**:
1. In base alla politica impostata dall’amministratore, ad ogni rotta è assegnata un valore di **preferenza locale**, e verranno scelte le rotte con preferenza più alta.
2. Si seleziona la rotta con valore **AS-PATH più breve**.
3. Si seleziona quella il cui router di NEXT-HOP ha costo minore (**hot-potato routing**).
4. Se rimane ancora più di una rotta, il router si basa sugli identificatori BGP.

## BGP Advertisement Ristretto (politiche)

 ![[Pasted image 20250607121219.png|900]]

Le reti `A`, `B`, `C` sono **provider networks**, ovvero [[#^45a215|AS di transito]] gestite da ISP [^1]  diversi che si occupa di fa transitare i pacchetti per connettere i *consumer network*.

Le reti `w`, `x`, `y` sono **consumer networks** servite dai provider network, ovvero reti in cui i pacchetti non devono transitare ma possono essere inviati e ricevuti.

>[!note] Policy Provider Network
>
>Generalmente, ogni provider network vuole instradare solo il traffico originato o diretto alle proprie consumer network, evitando che pacchetti esterni transitino diretti verso consumer network non serviti dal consumer network. 
>
>Per questo nel esempio precedente vengono applicate le seguenti policy:
>- `A` annuncia il percorso `Aw` ai vicini `B` e `C`.
>- `B` sceglie di non annunciare `BAw` a `C`, dato che `B` non ha alcun vantaggio a instradare `CBAw`, poiché nessuno tra `C`, `A` e `w` sono clienti di `B`.
>- Quindi `C` non scopre il percorso `CBAw`,  ma può sempre utilizzare `CAw` per raggiunger `w`.

>[!note] Policy Consumer Network
> Le reti `w` e `y` essendo [[#^dcda86|AS stub]] non hanno bisogno di policy particolari per evitare il transito di pacchetti.
> 
> Al contrario `x` essendo collegata a due provider ([[#^d78acf|multi-homed]]) deve attuare le seguenti politiche per evitare che i pacchetti transitino all'interno della sua rete:
>- `x` non vuole instradare da `B` a `C`, allora `x` non annuncia a `B` la rotta verso `C`.
>- `x` non vuole instradare da `C` a `B`, allora `x` non annuncia a `C` la rotta verso `B`.
## Messaggi BGP

I messaggi BGP vengono scambiati attraverso [[Protocollo TCP (Transmission Control Protocol)|TCP]], ci sono diversi tipi di messaggi:
- **OPEN** - Apre la connessione TCP e permette l’autenticazione del mittente
- **UPDATE** - Annuncia il nuovo percorso o cancella quello vecchio
- **KEEP-ALIVE** - Mantiene la connessione attiva in mancanza di UPDATE
- **NOTIFICATION** - Riporta gli errori del precedente messaggio oppure viene usato per chiudere il collegamento.

## Osservazioni Finale

>[!note] Perché inter-AS e intra-AS sono protocolli diversi?
> 
> Si vuole una diversa gestione delle politiche, negli inter-AS si vuole avere controllo di come si muove il traffico e chi lo muove. Negli intra-AS c’è un unico controllo amministrativo e quindi le scelta delle politiche è meno impattante.
> 
> Per quanto riguarda le prestazioni negli intra-AS vogliamo appunto più prestazioni mentre negli inter-AS le politiche possono prevalere sulle prestazioni.

[^1]: Internet Service Provider

