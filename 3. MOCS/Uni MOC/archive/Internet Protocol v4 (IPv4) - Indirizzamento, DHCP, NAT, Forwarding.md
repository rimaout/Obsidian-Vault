---
type: Uni Note
class: "[[Reti (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-05-08T15:55
updated: 2026-01-31T13:32
---
## Introduzione

Il protocollo IPv4 è responsabile della *suddivisione in pacchetti*, dell’inoltro (*forwarding*), e della *consegna* dei datagrammi al livello di rete (host to host).

È un protocollo **inaffidabile**, *non orientato alla connessione* e *basato su datagrammi*, offre un servizio **best effort**.

>[!note] Formato Datagramma
>
>![[Pasted image 20250508160055.png|700]]
>
>- ***Numero di versione***: consente al router la corretta interpretazione del datagramma, assume i valori `4` (IPv4) o `6` ([[Internet Protocol v6 (IPv6)|IPv6]]).
>- ***Lunghezza dell’intestazione***: utilizzato per indicare dove inizia il campo dati, questo perché un datagramma IP può contenere un numero variabile di opzioni (incluse nell’intestazione).
>- ***Tipo di servizio***: serve per distinguere diversi datagrammi con requisiti di qualità del servizio diverse (realtime)
>- ***Lunghezza del datagramma***: lunghezza totale (in byte) del datagramma IP inclusa l’intestazione. Serve per capire se il pacchetto è arrivato completamente.
>- ***Identificatore***, ***flag*** e ***offset di frammentazione***: questi tre campi servono per gestire la frammentazione dei pacchetti ([[Internet Protocol v6 (IPv6)|IPv6]] non prevede frammentazione).
>- ***Tempo di vita***: o time to live (TTL) assicura che i datagrammi non restino in circolazione per sempre nella rete. Il campo viene ddecrementato a ogni hop e il datagramma viene eliminato in caso il suo `TTL = 0`.
>- ***Protocollo***: indica il protocollo a livello di trasporto al quale va passato il datagramma. Questo campo è utilizzato solo quando il datagramma raggiunge la destinazione finale. (es. TCP, UDP, ICMP, IGMP, OSPF)
>- ***Checksum dell’intestazione***: consente ai router di rilevare errori sui datagrammi ricevuti.
>- ***Indirizzi IP di origine e destinazione***: inseriti dall’host che crea il datagramma (dopo aver effettuato una ricerca DNS).
>- ***Opzioni***: campi che consentono di estendere l’intestazione IP, usati per test o debug della rete.
>- ***Dati***:  il campo dati contiene il segmento di trasporto da consegnare alla destinazione.

## Frammentazione 

Un datagramma IP può dover viaggiare in più reti, tutte con caratteristiche diverse fra loro. Ogni router estrae il datagramma dal frame, lo elabora e lo incapsula in un nuovo frame.

Un caratterista importante che può variare, in base alla tecnologia, è la **Maximum Transfer Unit** (MTU) è la massima quantità di dati che un frame a livello di collegamento può trasportare.

![[Pasted image 20250508161427.png|700]]

Grazie alla frammentazione, grandi datagrammi IP vengono frammentati in datagrammi IP più piccoli, processo:
1. Datagramma viene frammentato.
2. I frammenti verranno riassemblati soltanto a destinazione.
3. Vanno riassemblati prima di raggiungere il livello di trasporto.
4. I bit dell’intestazione IP sono usati per identificare e ordinare i frammenti.

Quindi quando un host riceve una serie di datagrammi dalla stessa origine deve:
1. Individuare i frammenti
2. Determinare quando è arrivato l’ultimo
3. Stabilire l’ordine di assemblaggio

Per effettuare questi procedimenti vengono utilizzate delle informazioni aggiuntive:
- **Identificazione (16 bit)** - Identificativo associato ad ogni datagramma al momento della sua creazioni, che identifica tutti i frammenti generati dalla stesso datagramma.
- **Flag (3 bit)**
	1. *Il primo*: è riservato (?)
	2. *Il secondo* se vale `1` indica che il datagramma non va frammentato, `0` si può frammentare.
	3. *Il terzo* se vale `1` indica che è un frammento intermedio, `0` se ultimo frammento.
- **Offset** - specifica l’ordine del frammento all’interno del datagramma originario.

>[!note] Calcolo dell'offset
>
>Calcoliamo gli offset di tre frammenti generati da un datagramma con un payload di dimensione 4000 byte.
>
>>***nota:*** l'offset in questo caso è misurato in unità da 8 byte.
>>
>>![[Pasted image 20250508162759.png|700]]

^f1e168

>[!note] Esempio frammentazione
>
>Prendendo il datagramma e i frammenti dell'[[#^f1e168|esempio precedente]], vediamo come avviene la frammentazione.
>
>![[Pasted image 20250508162942.png|700]]
>
>Può anche avvenire:
>
>![[Pasted image 20250508163535.png|700]]

^f2b5a2

---
## Indirizzamento IPV4

Ogni *interfaccia di host* e *router di Internet* ha un indirizzo IP globalmente univoco detto indirizzo IP. 

**Interfaccia != dispositivo:** un interfaccia è il confine tra il dispositivo e l’esterno, questo significa che un singolo dispositivo può avere più indirizzi se ha più interfacce, ad esempio sistema sia con un interfaccia via cavo (Ethernet) che una wireless.

**Numero di Indirizzi:** L' indirizzo IP essendo composto da 32 bit (4 byte) permette di avere `2^32` ovvero **4 miliardi** di indirizzi univoci diversi.

>[!note] Notazione Indirizzi
>
>È possibile rappresenta un stesso indirizzo IP con 3 notazioni differenti:
>- ***Binaria***
>- ***Decimale puntata*** dove ognuno dei 4 byte è rappresentato da un numero compreso tra `0-255`.
>- ***Esadecimale*** molto utilizzata nella programmazione di rete
>  
>![[Pasted image 20250508172518.png|500]]

>[!note] Gerarchia
>
>Un indirizzo è diviso in:
>- **Prefisso**: si scelgono `n bit` da sinistra che individuano la rete
>- **Suffisso**: i restanti `32−n bit` individuano l’interfaccia all’interno della rete
>  
>![[Pasted image 20250508173037.png|500]]

Esistono due modi per effettuare indirizzamento:
- [[#Indirizzamento con Classi]]
- [[#Indirizzamento senza Classi]]

### Indirizzamento con Classi

La dimensione del prefisso è limitata a tre valori, premettendo di supportare sia reti piccole che grandi.

- ***Classe A*** - Prefisso da `8 bit` e il primo byte va da 0 a 127
- ***Classe B*** - Prefisso da `16 bit` e il primo byte va da 128 a 191
- ***Classe C*** - Prefisso da `24 bit` e il primo byte va da 192 a 223
- ***Classe D*** - Non ci sono prefissi e suffissi ma sono degli indirizzi speciali di multicast ovvero per inviare messaggi a tutta la rete. Il primo byte va da 224 a 239

![[Pasted image 20250508173546.png|600]]

Un **vantaggio** di questo metodo è che una volta individuato un indirizzo si risale facilmente alla classe e alla lunghezza del prefisso.

Lo **svantaggio** principale è l'esaurimento degli indirizzi infatti:
- La ***classe A*** può essere assegnata solo a 128 organizzazioni al mondo, ognuna con 16.777.216 nodi. Un numero nodi che difficilmente può essere sfruttato da una singola organizzazione.
- La ***classe B*** ha lo stesso problemi della A ma in una scala minore.
- La ***classe C*** al contrario ha pochi indirizzi (256) per rete.

Per questo in Internet si usa un [[#Indirizzamento senza Classi|indirizzamento senza classi]].

### Indirizzamento senza Classi

L’indirizzamento senza classi è nato per avere maggiore flessibilità nel assegnamento degli indirizzi. Per questo il prefisso è di lunghezza variabile (da 0 a 32 bit) e per identificarne la lunghezza si utilizza la [[#^6f080f|notazione CIDR]].

>[!note] Notazione CIDR (Classless InterDomain Routing)
>
>L'indirizzo IP è diviso in una struttura `a.b.c.d/n`, dove:
>- `a.b.c.d` sono i byte del indirizzo vero e proprio.
>- `n` indica il numero di bit (non byte) che rappresentano il prefisso.
>  
>>***Esempio:*** $200.23.16.0/23 \to \underbrace{11001000\ \ 00010111\ \ 0001000}_{\text{Prefisso} }\underbrace{0\ \ 0000000}_{\text{Sufisso}}$
>
>Se `n` è la lunghezza del prefisso allora possiamo ricavare varie informazioni:
>- Il numero di indirizzi nel blocco (rete) è dato da $N = 2^{32}-1$
>- Per trovare il primo indirizzo nella rete si impostano a 0 tutti i bit del suffisso
>- Per trovare l’ultimo indirizzo nella rete si impostano a 1 tutti i bit del suffisso

^6f080f

>[!note] Maschera dell'indirizzo
>
>La maschera dell’indirizzo è un numero da 32 bit dove i primi `n bit` a sinistra (il prefisso) sono impostati a 1 mentre i restanti a 0, grazie alla maschera si ottiene l’*indirizzo* di rete usato nell’*instradamento dei datagrammi verso la destinazione*.
>
>Attraverso la maschera, utilizzando delle operazioni, è possibile ricavare le seguenti informazioni di un blocco:
>- Numero degli indirizzi del blocco `N = NOT(maschera)+1`
>- Primo indirizzo del blocco `(qualsiasi indirizzo) AND (maschera)`
>- Ultimo indirizzo del blocco `(qualsiasi indirizzo) OR (NOT(maschera))`
>  
>>***Esempio:*** Una maschera da /24 bit è 255.255.255.0 e indica che i primi 24 bit sono per la rete:
>>
>>Con l’operazione `NOT` otteniamo `0.0.0.255` che in binario è `0000000.00000000.00000000.11111111` e aggiungendo uno otteniamo `256` ovvero gli indirizzi disponibili in quella sottorete.
 
>[!note] Indirizzi Speciali
>
>- L’indirizzo `0.0.0.0` è utilizzato dagli host al momento del boot
>- Gli indirizzi IP che hanno tutti `0` come numero di rete si riferiscono alla rete corrente
>- L’indirizzo composto da tutti `1` permette la trasmissione broadcast sulla rete locale (in genere una LAN)
>- Gli indirizzi con numero di rete opportuno e tutti `1` nel campo host permettono l’invio di pacchetti broadcast a LAN distanti
>- Gli indirizzi nella forma `127.xx.yy.zz` sono riservati al loopback (questi pacchetti non vengono immessi nel cavo ma elaborati localmente e trattati come pacchetti in arrivo)

>[!note] Richieda di un indirizzo di Rete
>
>Un amministratore di rete, per ottenere un blocco di indirizzi liberi da usare in una rete deve contattare il suo ISP. In questo modo otterrà un blocco di indirizzi contigui con un prefisso comune nella forma `a.b.c.d/n` dove `n` è la maschera di indirizzo.
>
>Ma l’ISP da dove ottiene il blocco di indirizzi? C’è un organizzazione che gestisce questo aspetto e anche i server DNS root chiamata **ICANN** (Internet Corporation for Assigned Names and Numbers).

#### DHCP

Per decidere qual è l'indirizzo da assegnare ad un dispositivi (interfaccia) in una rete abbiamo 2 metodi:
- ***Assegnazione manuale*** - Eseguita una volta per dispositivo che manterrà sempre lo stesso indirizzo nella rete
- ***DHCP (Dynamic Host Configuration Protocol)*** 
 
 Il protocollo **DHCP** consente ad un host di ottenere automaticamente (*plug-and-play*) un indirizzo IP ogni qualvolta si collega alla rete.
 
 Di default ogni volta che il dispositivo si collega alla rete gli viene assegnato un indirizzo potenzialmente diverso (indirizzo dinamico), anche se esistono metodi per associare degli indirizzi IP fissi a determinati postitivi (indirizzi fisso).
- Questa tecnica consente il riuso degli indirizzi, permettendo di avere una quantità di indirizzi inferiore rispetto al numero totale di utenti.
- Ad esempio: collegandomi alla rete ottengo l’indirizzo `x`, una volta sconnesso l'indirizzo `x` torna ad essere libero e può essere riutilizzato da altri host.

Le informazioni fornite dal DHCP all'host sono:
- Indirizzo IP
- Maschera di Rete
- Indirizzo del router
- Indirizzo DNS
 
>[!note] Funzionamento DHCP
>
>Il DHCP è un protocollo client server dove:
>- Un ***Client*** è un host appena connesso che desidera ottenere informazioni sulla configurazione della rete, non solo un indirizzo IP
>- Il ***Server***, ogni sottorete dispone di un server DHCP, se questo non è presente è il router ad agire da server.
>
>Quando un host si collega alla rete:
>1. L’host invia un messaggio broadcasts `DHCP discover`.
>2. Il server DHCP risponde con `DHCP offer`
>3. L’host richiede l’indirizzo IP con `DHCP request`
>4. Il server DHCP invia l’indirizzo `DHCP ack`

>[!note] Formato dei messaggi DHCP
>
>![[Pasted image 20250509102153.png|1000]]
>
>>***Nota:*** non è previsto un campo per specificare il tipo di messaggio, per questo scopo si utilizza un magic cookie nel campo opzioni pari a `99.130.83.99`.

>[!example] Esempio
>
>![[Pasted image 20250410145130.png|700]]
>
>Il ***client*** è una macchina appena connessa alla rete e richiede un indirizzo IP.
>- Non sapendo chi è il server DHCP o il server DNS, fa una richiesta broadcast diretta a tutti i nodi della rete (*destination address*: `255.255.255.255`).
>- Non avendo un proprio indirizzo IP, utilizza come *source address* tutti 0.
>
>Il ***server*** DHCP, una volta ricevuta la richiesta:
>- Invia una risposta contenente l’indirizzo da assegnare al client (in questo caso: 181.14.16.182).
>- Viene mandata in broadcast (255.255.255.255) a tutti i nodi della rete, visto che il client che ha effettuato la richiesta non conosce ancora il suo indirizzo IP.
>
>Il ***client*** riceve la risposta contenente il suo nuovo indirizzo IP e altre informazioni, tra cui l'indirizzo IP del server:
>- Invia la conferma di ricevimento, ma questa risposta non viene inviata a tutti i nodi della rete (broadcast); allo stesso tempo, non viene inviata solo al server che gli ha assegnato l'indirizzo IP.
>- Questo perché in una rete possono esserci più server DHCP, ognuno dei quali, dopo aver ricevuto la richiesta dal client, aveva generato precedentemente un indirizzo per il client.
>- Il client utilizza come indirizzo IP il primo che riceve, ma deve notificare tutti gli altri server DHCP in modo tale che sappiano che l’indirizzo IP da loro generato non è stato utilizzato e che quindi potrà essere utilizzato per qualche altro dispositivo.
>
>>***Nota:***
>>- Per gestire queste richieste il DHCP usa delle **well-known** port ovvero `68` in ascolto sul client e `67` in ascolto sul server-
>>- Per distinguere gli host tra loro si utilizzano informazioni aggiuntive come l'indirizzo MAC, altrimenti nel caso di client che si collegano nello stesso momento si potrebbero creare conflitti. Ad esempio due host interpretano lo stesso messaggio di risposta del server come destinato a loro.

## Nat

Prima dobbiamo definire il concetto di **Sotto Rete**, una rete isolata i cui punti terminali sono
collegati all’interfaccia di un host o di un router.

In particolare all’interno della stessa sottorete gli host devono avere tutti lo stesso prefisso ad esempio nella sottorete `223.1.1.0/24` tutti i terminali devono iniziare con `223.1.1.xxx`.

>[!warning] Probelma
>
>Questa [[#Indirizzamento senza Classi|notazione CIDR]] ha reso più flessibile l’assegnazione di blocchi ma ha anche creato un problema, se in futuro si ha bisogno di più indirizzi e il blocco successivo è occupato come si fa?
>
>Per questo è stato inventati i concetti di [[#Indirizzo Privato|indirizzo privato]] e [[#Traduzione degli indirizzi di rete (NAT)|traduzione degli indirizzi di rete (NAT)]].

### Indirizzo Privato

Gli indirizzi IP privati sono delle classi di indirizzi IPv4 riservati esclusivamente per le reti locali.

Chiunque può utilizzare questi indirizzi per la propria rete locale, perché i pacchetti con tali indirizzi non vengono utilizzati per l'indirizzamento e instradamento dai [[Introduzione al Livello di Rete#Router|router]] Internet.

Nel caso occorra connettere ad Internet una rete locale che utilizza queste classi di indirizzi si deve ricorrere al [[#Traduzione degli indirizzi di rete (NAT)|network address translation (NAT)]].

>[!note] Classi indirizzi privati
>
>Le tre classi in questione sono:
>
>| Nome         | Indirizzo iniziale | Indirizzo finale | Classi                | Blocco CIDR più grande (subnet mask) | ID Rete | ID Host | Numero di indirizzi disponibili |
>| ------------ | ------------------ | ---------------- | --------------------- | ------------------------------------ | ------- | ------- | ------------------------------- |
>| 24-bit block | 10.0.0.0           | 10.255.255.255   | Singola classe A      | 10.0.0.0/8 (255.0.0.0)               | 8 bit   | 24 bit  | 16.777.216                      |
>| 20-bit block | 172.16.0.0         | 172.31.255.255   | 16 classi B contigue  | 172.16.0.0/12 (255.240.0.0)          | 12 bit  | 20 bit  | 1.048.576                       |
>| 16-bit block | 192.168.0.0        | 192.168.255.255  | 256 classi C contigue | 192.168.0.0/16 (255.255.0.0)         | 16 bit  | 16 bit  | 65.536                          |

### Traduzione degli indirizzi di rete (NAT)

L'acronimo NAT sta per **Network Address Translation**, i router abilitati al NAT nascondono i dettagli della rete domestica al mondo esterno.

Grazie a questa tecnologia è possibile:
- Non è necessario allocare un intervallo di indirizzi da un ISP, un unico indirizzo IP è sufficiente per tutte le macchine di una rete locale.
- È possibile cambiare gli indirizzi delle macchine di una rete privata senza doverlo comunicare all’Internet globale.
- È possibile cambiare ISP senza modificare gli indirizzi delle macchine della rete privata.
- Dispositivi interni alla rete non esplicitamente indirizzabili e visibili dal mondo esterno (garantisce maggiore sicurezza).

>[!note] Implementazione
>
>Quando un router con NAT riceve il datagramma:
>- sostituisce l’indirizzo IP origine (dell’host) con il proprio indirizzo IP (router) sul lato WAN 
>- genera per esso (il datagramma) un nuovo *numero di porta d’origine*, e sostituisce il numero di porta origine iniziale con il nuovo numero appena generato\
>
>![[Pasted image 20250510135047.png|700]]
> 
>Quindi viene utilizzato il numero di porta non con il suo scopo originale (identificare dei processi) ma per identificare le diverse connessioni che partono da host diversi all'interno della rete locale e che vengono instradate verso la stessa destinazione sul lato WAN, consentendo al router di distinguere e instradare correttamente i pacchetti di ritorno ai rispettivi host di origine.
>
>>***Nota:*** Il campo numero di porta è lungo 16 bit, quindi attraverso protocollo NAT può supportare più di 60.000 connessioni simultanee con un solo indirizzo IP sul lato WAN.

>[!bug] Criticità
>
>Il numero di porta viene usato per identificare host e non processi, questo porta alcuni proplemi:
>1. I router dovrebbero elaborare i pacchetti solo fino al livello 3 (rete) ma il numero di porta fa parte del livello 4 (trasporto).
>2. Viola il cosiddetto argomento punto-punto, ovvero gli host dovrebbero comunicare tra di loro direttamente, senza intromissione di nodi né modifica di indirizzi IP e numeri di porta.
>3. Il NAT crea problemi con le app P2P in cui ogni peer dovrebbe essere in grado di avviare una connessione TCP con qualsiasi altro peer. A meno che il NAT non sia specificamente configurato per quella specifica applicazione P2P.

## Forwarding

Inoltrare (forwarding) significa **collocare il datagramma sul giusto percorso** che lo porterà a destinazione o comunque procedere verso essa.

Quando un host deve inviare un datagramma all’esterno della rete lo invia al router della rete locale il quale accede alla tabella di routing per trovare il successivo hop a cui inviarlo, l’inoltro richiede una riga nella tabella per ogni blocco di rete.

Ad esempio:

![[Pasted image 20250510165808.png|550]]

Il router R1 avrà una tabella, del tipo:

| Indirizzo di Rete | Hop successivo | Interfaccia |
| ----------------- | -------------- | ----------- |
| 180.70.65.192/26  | -              | m2          |
| 180.70.65.128/25  | -              | m0          |
| 201.4.22.0/24     | -              | m3          |
| 201.4.16.0/22     | -              | m1          |
| default           | 180.70.65.200  | m2          |

>***Nota:*** Gli indirizzi sono ordinati per la grandezza del prefisso (dal più grande al più piccolo)

Ogni volta che il router riceve un datagramma deve decidere su che interfaccia instradarlo, per fare ciò effettua una ricerca sui *Indirizzi di Rete* presenti nella tabella routing e cerca quello "compatibile".

>[!note] Determinare l'indirizzo "compatibile"
>
>Arriva al router un datagramma con destinazione `180.70.65.140`, ora dobbiamo capire su quale interfaccia del router va instradato.
>
>Per fare ciò dobbiamo riscrivere tutti gli indirizzi della tabella e della destinazione del datagramma, prendendo in considerazione soltanto il prefisso e mostrandolo in binario.
>
>Quindi la tabella diventa:
>
>|Bit a sinistra nell'indirizzo di destinazione|Salto successivo|Interfaccia|
>|---|---|---|
>|10110100 01000110 01000001 11|-|m2|
>|10110100 01000110 01000001 1|-|m0|
>|11001001 00000100 00011100|-|m3|
>|11001001 00000100 000100|-|m1|
>|Default|180.70.65.200|m2|
>
>
>L'indirizzo di destinazione del datagramma: `10110100 01000110 01000001 10001100`.
>
>Per determinare quale tra gli indirizzi della tabella è compatibile, partiamo dal più lungo e li confrontiamo:
>
>$$
>\begin{align*}
>&\text{indirizzo dest: } 10110100\ 01000110\ 01000001\ 1\textcolor{orange}{0}001100 \\
>&\text{indirizzo tabl: } ​10110100\ 01000110\ 01000001\ 1\textcolor{orange}{1}​\\
>\end{align*}
>$$
>
>In questo uno dei bit (quello in arancione) non combacia, quindi tentiamo con l’indirizzo successivo.
>
>$$
>\begin{align*}
>&\text{indirizzo dest: } 10110100\ 01000110\ 01000001\ 10001100 \\
>&\text{indirizzo tabl: } 10110100\ 01000110\ 01000001\ 1\\
>\end{align*}
>$$
>
>In questo caso i due indirizzi combaciano quindi la 2° riga della tabella è quella compatibile e quindi il datagramma verrà instradato sull’interfaccia `m0`.

>[!note] Aggregazione degli indirizzi
>
>Inserire nella tabella una riga per ogni blocco può portare a tabelle molto lunghe, con aumento del tempo necessario per fare la ricerca. Per risolvere il problema si usa l’**aggregazione degli indirizzi**.
>
>![[Pasted image 20250511163246.png|600]]
>
>Notiamo che le 4 società hanno 4 blocchi di indirizzi contigui, le raggruppiamo quindi in un router che le gestisce (R1) e all’interno di R2 eseguiamo una mappatura su una maschera che le contiene tutte, con interfaccia di uscita sul router R1.
>
>In questo modo abbiamo meno entry sul tabella di R2 e soltanto 4 in quella di R1.
>
>Quindi nella tabella di R2 avremo soltanto la seguente riga:
>- *Indirizzo:* 140.24.7.0/24
>- *Next Hop:* Indirizzo R1
>- *interfaccia:* m0
>
>È importante ricordare che:
>- Per eseguire l’aggregazione le reti devono essere contigue
>- Devono avere tutte lo stesso next-hop
>- Il prefisso aggregato deve contenere soltanto tutte le reti originale