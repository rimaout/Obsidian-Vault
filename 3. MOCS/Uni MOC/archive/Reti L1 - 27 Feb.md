---
type: Uni Note
class:
  - "[[Reti (class)]]"
academic year: 2024/2025
related: 
completed: false
created: 2025-02-27T14:31
updated: 2025-02-28T14:09
---
file:///Users/mr/Downloads/lezione_1_Reti.pdf

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

>[!note] Rete di comunicazione di pacchetto
>
>Metodo su cio si base l'attuale rete internet
>
>non viene riservato nessun tipo di risorsa ma si vanno a suddividere i dati.
>
>I dati che vogliamo trasmettere vengono suddivse in blocchi ovvero "piccole parti" chiamate pacchetti.
>
>I router che ricevono i dati dagli utenti li inseriscono ad una coda (store) ed li inviano nella rete in modo sequenziale (forward). 

^d8b0c9

## Struttura concettuale di Internet

## Rete di accesso
