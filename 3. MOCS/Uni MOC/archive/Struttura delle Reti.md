---
type: Uni Note
class:
  - "[[Reti (class)]]"
academic year: 2024/2025
related: 
completed: true
created: 2025-03-11T10:57
updated: 2025-04-11T11:52
---
## Rete

Una rete è composta da noti, ovvero dispositivi capaci di scambiarsi informazioni che vengono categorizzati in *sistemi terminali* e *dispositivi di interconnessione* che sono collegati tra loro attraverso dei *collegamenti* detti link.

I **sistemi terminali** possono essere di due tipi:
- *Host* - macchine generalmente di proprietà dell'utente dedicate ad eseguire applicazioni.
- *Server* - tipicamente è una macchina ad elevate prestazioni destinata a fornire servizi a diverse applicazioni utente.
  
I **dispositivi di interconnessione** rigenerano/modificano il segnale che ricevono e lo ridistribuiscono: ^d03292
- *Router* - collegano una rete ad altre reti
- *Switch* - (commutatori) collegano più sistemi terminali a livello locale
- *Modem* - trasformano la codifica dei dati

## Mezzi Transitivi

I **collegamenti** chiamati genericamente link sono mezzi transitivi utilizzati per collegare dispositivi di rete, ne esistono di due tipi:
- *cablati* (o guidati) - solitamente in rame o fibra ottica
- *wireless* - onde elettromagnetiche o satellite

>[!note] Mezzi Transitivi Cablati
>
>I segnali si propagano in un mezzo che collega fisicamente due dispositivi. Alcuni di questi mezzi sono:
>
>**1) Doppio Intreccio** - (TP: twister pair) due fili di rame distinti, il tradizionale cavo telefonico.
>
>**2) Ethernet** - intreccio di quattro coppie di fili.
>
>**3) Cavo Coassiale:** 
>- Due conduttori in rame concentrici capace di propagare il segnale bidirezionalmente.
>- Era usato per cablatura reti locali ad alta velocità perché resistente alle interferenze, ma oggi è stato soppiantato dalla fibra ottica.
>
>**4) Fibra Ottica:** 
>- Mezzo sottile e flessibile che conduce impulsi di luce (ciascun impulso rappresenta un bit).
>- È caratterizzato da un alta frequenze trasmissiva e un basso tasso di errore perché non subisce interferenze elettromagnetiche.
>- Mezzo prevalente delle dorsali internet.

>[!note] Mezzi Transitivi Wireless
>
>Anche detti mezzi ad onda libera, i segnali si propagando bidirezionalmente nell'atmosfera e nello spazio esterno attraverso onde elettromagnetiche.
>
>I segnali sono influenzati dall’ambiente di propagazione: riflessione, ostruzione da parte di ostacoli, interferenze da altri segnali.
>
>I principali canali radio sono:
>
>- **Microonde Terrestri** - es. canali fino a 45 Mbps
>- **LAN** - es. Wifi-IEEE802.11
>- **Wide-area** - es. cellulari
>- **Satellitari** - canali fino a 45 Mbps channel con ritardo punto-punto di 270 msec sono creati da satelliti geostazionari/a bassa quota.

## Classificazione delle reti

| Scale    | Type                                   |                           |
| -------- | -------------------------------------- | ------------------------- |
| Vicinity | PAN (Personal Area Network)            | Bluetooth (e.g., headset) |
| Building | LAN (Local Area Network)               | WiFi, Ethernet            |
| City     | MAN (Metropolitan Area Network)        | Cable, DSL                |
| Country  | WAN (Wide Area Network)                | Large ISP                 |
| Planet   | The Internet (network of all networks) | The Internet!             |

### Reti LAN

Solitamente è una rete privata che collega i sistemi terminali di un singolo edificio, deve ogni sistema terminale nella LAN ha un indirizzo che lo identifica univocamente nella rete.

>***oss:*** non specifica un numero minimo o massimo di dispositivi.

Esistono due tipi di strutture LAN :
- con cavo condiviso (mezzo broadcast)
- a commutazione (con switch) ^c5f4ee

>[!note] Rete LAN Broadcast 
>
>Quando un nodo trasmette tuti i terminali nella rete ricevono la trasmissione, dove solo il destinatario elabora il pacchetto, tutti gli altri lo ignorano. 
>
>In questa struttura *solo un nodo alla volta può trasmettere* e per questo al giorno d'oggi è **obsoleta**.
>
>![[Pasted image 20250228100958.png|900]]

>[!note] Reti LAN con Switch
>
>Ogni nodo della LAN è collegato direttamente ad uno switch, in questa struttura *soltanto il destinatario riceverà la trasmissione* del trasmettitore.
>
>Questo avviene grazio allo switch che effettua da **intermediario** è in grado di riconoscere l’indirizzo di destinazione e di inviare il pacchetto al solo destinatario senza inviarlo agli altri dispositivi.
>
>Lo switch riduce il traffico nella LAN e consente a più coppie di dispositivi di *comunicare contemporaneamente* fra di loro.
>
>![[Pasted image 20250228101214.png|640]]

### Rete WAN

La rete WAN (Wide Area Network) è una rete che interconnette dispositivi di [[#^d03292|interconnessione]] (switch, router, modem) su una grande area geografica (città, una regione, o una nazione).

Questo tipo di rete è gestita da un **operatore di telecomunicazioni** (Internet Service Provider - **ISP**).

Ne esistono di due tipi la [[#^5c7f8d|punto a punto]] e [[#^21f93e| a commutazione]].

>[!note] Rete Punto a Punto
>
>Collega semplicemente due mezzi di comunicazione tramite un mezzo trasmissivo (cavo o wireless)
>
>![[Pasted image 20250228103916.png|600]]

^5c7f8d

>[!note] Rete a Commutazione
>
>Rete con più di due punti di terminazione, è utilizzata nelle dorsali di Internet.
>
>![[Pasted image 20250228104022.png|600]]

^21f93e

### Reti Composte (Internetwork)

Oggi giorno è difficile trovare LAN o WAN isolate: esse sono in genere connesse fra di loro per formare una internetwork, o internet.

>[!example] Esempio - Due LAN e una WAN punto-punto
>
>Un’azienda ha due uffici in due città differenti. In ciascun ufficio esiste una LAN che consente agli impiegati di comunicare l’uno con l’altro. 
>
>Per mettere in comunicazione le due LAN l’azienda affitta un’apposita WAN punto-punto da un ISP, realizzando una internet privata.
>
>![[Pasted image 20250228104529.png|900]]

>[!example] Esempio - Quattro WAN e tre LAN
>
>
>
>![[Pasted image 20250228104735.png|800]]

>[!note]- Approfondimento rete GARR
>
>La rete GARR interconnette ad altissima capacità università, centri di ricerca, biblioteche, musei, scuole e altri luoghi in cui si fa istruzione, scienza, cultura e innovazione su tutto il territorio nazionale. 
>
>È un’infrastruttura in fibra ottica che utilizza le più avanzate tecnologie di comunicazione e si sviluppa su circa 15.000 km tra collegamenti di dorsale e di accesso.
>
>Oggi la capacità delle singole tratte della dorsale arriva a 100 Gbps, mentre quella dei collegamenti di accesso può raggiungere i 40 Gbps in base alle necessità di banda della sede. 
>
>Grazie alla grande scalabilità delle tecnologie utilizzate, queste capacità possono evolvere facilmente insieme alle necessità degli utenti. 
>
>**Sito GARR:** http://www.garr.it/it/infrastrutture/rete-nazionale/infrastruttura-direte-nazionale

## Comunicazione (Switching)

Una internet (internetwork) è una combinazione di link e dispositivi capaci di scambiarsi informazioni. In particolare i sistemi terminali comunicano tra di loro per mezzo di dispositivi come switch e router.

Ci sono due tipi di reti basate su switch:
- [[#^25f8b9|Reti a comunicazione di circuito]]
- [[#^d8b0c9|Rete di comunicazione di pacchetto]]

>[!note] Reti a commutazione di circuito
>
>Tra due dispositivi è sempre disponibile un collegamento dedicato chiamato **circuito**, *utilizzato per l'intera comunicazione*.
>
>Stabilire un circuito significa riservare le risorse fisiche necessarie per effettuare il collegamento tra i due dispositivi. Queste risorse saranno inaccessibili a gli altri dispositivi per tutto il tempo necessario per effettuare la comunicazione.
>
>**Percorso** - anche se esistono più percorsi tra due dispositivi in comunicazione, solo uno di questi verrà usato per l’intera comunicazione
>
>**Efficenza** - questo tipo di comunicazione ci assicura che le risorse fisiche siano "prenotate" per tutto il tempo delle comunicazione.
>
>Le risorse della rete (es. ampiezza di banda) possono essere suddivise in "pezzi". La banda in particolare può essere divisa in due modi per frequenza (**FDM**) o per tempo (**TDM**).
>
>>***FDM (Frequency Division Multiplexing)***
>>
>>![[Pasted image 20250228121344.png|600]]
>
>>***TDM (Time Division Multiplexing)***
>>
>>![[Pasted image 20250228121504.png|600]]

^25f8b9

>[!note] Rete di comunicazione di pacchetto (store and forward)
>
>La comunicazione fra i due lati, invece di avvenire in modo continuaviene effettuata trasmettendo blocchi di dati chiamati pacchetti.
>
>Gli switch memorizzano i dati ricevuti dagli utenti in una coda (store) e  li inoltrano nella rete in modo sequenziale (forward).
>
>![[Pasted image 20250302223106.png|600]]
>
>>***oss:*** non viene riservato nessun tipo di risorsa ma si vanno a suddividere i dati.
>
>---
>
>Non c’è un **percorso** specifico che viene usato per il trasferimento di dati tra due dispositivi. 
>
>Blocchi di dati, anche dello stesso file o comunicazione, possono prendere percorsi diversi nel viaggio dalla sorgente alla destinazione e arrivare a destinazione in un ordine diverso.
>
>![[Pasted image 20250302224616.png|700]]

^d8b0c9

## Internet

Con la parola **internet** (con i minuscola) ci si riferisci ad una rete composta da reti intercorresse. L’internet più famosa è chiamata **Internet** (I maiuscola) ed è composta da migliaia di reti interconnesse.

>***oss:*** È una rete a commutazione di pacchetto.

>[!note] Rappresentazione concettuale di Internet
>
>![[Pasted image 20250302224953.png|650]]

### Acesso ad Internet

Internet è una internetwork che consente a qualsiasi utente di farne parte. L’utente, tuttavia, deve essere fisicamente collegato a un ISP, solitamente mediante una WAN punto-punto.

Il collegamento che connette l’utente al primo router di Internet è detto **rete di accesso**, esistono 4 principali tecnologie per "collegarsi" ad una rete di accesso:
- [[#^d1e4d5|Accesso tramite rete telefonica]]
- [[#^7f0288|Accesso tramite Ethernet]]
- [[#^06c125|Accesso Wireless]]

>[!note] Accesso tramite rete telefonica
>
>E’ possibile collegarsi a Internet modificando la linea telefonica fra la sede del dispositivo che vuole connettersi (casa, azienda, etc.) e la centrale telefonica con una WAN punto-punto. Esistono due principali tecniche servizio **dial-up** e servizio **DSL**.
>
>>Servizio **dial-up** consiste nel inserire sulla linea telefonica un modem (modulatore-demodulatore) che converte i dati digitali (del computer) in analogici (per trasmetterli sulla linea telefonica) e viceversa.
>>
>>Lento e rende impossibile effettuare chiamate telefoniche e navigare internet contemporaneamente.
>>
>>![[Screenshot 2025-03-03 at 08.30.26.png|800]]
>
>>Servizio **DSL** (Digital Subscriber Line) tecnologia che supporta la comunicazione digitale ad alta velocità sulla linea telefonica.
>>
>> Il segnale tra abitazione e ISP è diviso tre bande di frequenza non sovrapposte ognuna con un compito specifico.
>> 
>> ![[Pasted image 20250303115019.png|700]]

^d1e4d5

>[!note] Accesso tramite Ethernet
>
>Nelle reti aziendali e universitarie una delle tecnologie utilizzate per l'accesso internet è il collegamento Ethernet.
>
>Lo switch (Ethernet) della LAN è generalmente collegato a un router istituzionale che è connesso diretamente ai router della dorsale.

^7f0288

>[!note] Accesso Wireless
>
>Il **wi-fi** è un Access Point (locale) connesso alla Ethernet cablata e ha un raggio di azione di qualche decina di metri.
>
>La **rete cellulare** ha un access point (base station) molto potente della compagnia telefonica cellulare, con raggio di azioni di decine di kilometri.

^06c125
## Access Network

Collegamenti fisici che connettono un sistema al primo **edge router**, un router esterno della rete [[#BackBome]].

![[Pasted image 20250303115524.png|400]]

>Nell'immagine gli edge router sono quelli in cui finiscono le line blu.

## BackBome

Solo router e collegamenti tra altri router, e può essere a [[#^25f8b9|Commutazione di circuito]] o [[#^d8b0c9|Commutazione di pacchetto]].

![[Pasted image 20250303120401.png|500]]

## Livello Rete ISP

La struttura di internet è una struttura gerarchica composta da reti di diverso livello, dove le reti sono gestite da **ISP** (Internet Service Provider).

>[!note] ISP Livello 1
>
>In cima ci gli ISP di livello 1 con *copertura nazionale ed internazionale* che comunicano tra loro alla pari (gestiscono [[#Dorsali Sottomarine]]).
>
>
>![[Screenshot 2025-03-11 at 10.41.39.png|300]]

>[!note] ISP Livello 2
>
>Le reti degli ISP di livello 2, sono reti con *copertura nazionale o distrettuale*. Si può connettere solo al alcuni ISP di livello 1, e possibilmente ad altri ISP di livello 2.
>
>![[Pasted image 20250311104634.png|700]]

>[!note] ISP Livello 3
>
>Le reti degli ISP di livello 3 sono *reti locali di accesso*, anche dette reti “ultimo salto” (last hop network), ovvero le più *vicine ai sistemi terminali*.
>
>![[Screenshot 2025-03-11 at 10.49.28.png|700]]

## Routing 

Il processo di determinare il percorso di un pacchetto all'interno della rete è detto **routing**.

![[Screenshot 2025-03-11 at 10.52.01.png|500]]

## Dorsali Sottomarine

![[Pasted image 20250228141445.png|600]]
