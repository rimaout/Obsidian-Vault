---
type: Uni Note
class: "[[Reti (class)]]"
academic year: 2024/2025
related: 
completed: true
created: 2025-03-20T12:15
updated: 2025-04-09T10:05
---
## Identificazione degli Host

Gli **host internet** hanno nomi detti hostname ad esempio `www.google.com` o `w3.uniroma1.it`, questi nomi sono facili da ricordare ma non ci danno informazioni sulla collocazione degli host all’interno di Internet.

Per la posizione di un **host internet** si utilizzano gli [[#Indirizzi IP]].
## Indirizzi IP

Gli **indirizzi IP** sono l’informazione che permette di determinare la vera posizione di un **host** nella rete. 

Possiamo rappresentarlo come una stringa dove ogni byte (4 byte = 32 bit) rappresenta un numero decimale compreso tra 0 e 255 ed ognuno di questi 4 numeri è separato da un `.` ad esempio: `121.34.230.94`.

Questo formato serve anche a creare una gerarchia negli indirizzi infatti vedremo che tramite l’indirizzo IP possiamo ricavare la rete di appartenenza e l’indirizzo del nodo.

Adesso ci serve un modo per determinare l'indirizzo IP di un host name e per questo si utilizzano i [[#Servizio DNS|servizi di DNS]].

## Servizio DNS

Un **servizio DNS** (Domain Name System) si occupa di convertire un *hostname* in un indirizzo *IP*.

![[Pasted image 20250318104943.png|700]]

>[!note] Memoria
>
>Il protocollo DNS associa ad ogni indirizzo IP un hostname,  però possono esistere $2^{32}$ indirizzi `IP` in totale come fa il `DNS` a memorizzarli tutti?
>
>Per quanto riguarda la **memorizzazione** si utilizza un **database distribuito** su una gerarchia di server DNS.

>[!warning] Applicazione o Protocollo?
>
>Si usa un **protocollo a livello applicazione** che consente agli host di interrogare i database dei server ed eseguire le traduzione.
>
>Il DNS viene utilizzato dagli altri protocolli di livello applicazione per tradurre gli hostname in indirizzi IP.
>
>Utilizza come protocollo per il trasporto l’[[Introduzione allo stack protocollare TCP-IP#^ad5398|UDP]] dato che ci serve più velocità che sicurezza per questo tipo di dati, di base utilizza la porta 53.
>

>[!example] Esempio
>
>Un browser (ossia client HTTP) di un host utente richiede la URL `www.someschool.edu`:
>1. L’host esegue il lato client dell’applicazione DNS
>2. Il browser estrae il nome dell’host `www.someschool.edu` dall'URL e lo passa al lato client dell'applicazione DNS
>3. Il client DNS invia una query contenente l’hostname a un server DNS
>4. Il client DNS riceve una risposta che include l’indirizzo IP corrispondente all’hostname
>5. Ottenuto l’indirizzo IP dal DNS, il browser può dare inizio alla connessione TCP verso il server HTTP localizzato a quell’indirizzo IP

## Aliasing

Permette di associare un nome più semplice da ricordare a un hostname complesso. Un host può avere uno o sinonimi (alias). 

Il DNS può essere invocato da un’applicazione per avere il nome canonico di un alias e il suo indirizzo IP

>[!example] Esempio
>
>L'hostname `relay1.west-coast.enterprise.compotrebbe` potrebbe avere due sinonimi, quali `enterprise.com` e `www.enterprise.com`, dove:
>- `relay1.west-coast.enterprise.compotrebbe` è detto hostname **canonico**
>- `enterprise.com` e `www.enterprise.comsono` sono gli alias

## Distribuzione del Carico

DNS viene anche utilizzato per distribuire il carico tra più server replicati.

I siti con molto traffico (es. cnn.com) vengono replicati su più server, e ciascuno di questi gira su un sistema terminale diverso e presenta un indirizzo IP differente:
- `151.101.3.5`
- `151.101.67.5`
- `151.101.131.5`
- `151.101.195.5`

>[!note] Funzionamento
>
>Ad un Hostname canonico (cnn.com) il DNS associa un insieme di indirizzi IP.
>
>Quando un client effettua un richiesta DNS per un hostname mappato ad un insieme di indirizzi, il server risponde con l’insieme di indirizzi ma variando l’ordinamento a ogni risposta questa rotazione permette di distribuisce il traffico sui server replicati.

## Server DNS Distribuiti

Ai tempi di ARPANET era un file `host.txt` che veniva caricato durante la notte al giorno d'oggi è basato su un struttura distribuita e gerarchica di server dove nessun server DNS mantiene il mapping per tutti gli host in Internet.

>[!note] Perché non si utilizza un singolo server?
>
>- Singolo punto di fallimento (tutto internet smette di funzionare)
>- Volume di traffico troppo elevato: un singolo server non potrebbe gestire tutte le querie DNS mondiali
>- Distanza dal database centralizzato: un singolo server non può essere fisicamente vicino a tutti i client
>- Manutenzione: il server dovrebbe essere aggiornato di continuo per includere nuovi nomi di host

Ci sono 3 classi di server DNS organizzati in una gerarchia:
- [[#^6085bc|Root]]
- [[#^60ff0c|Top-level domain (TLD)]]
- [[#^7c0b69|Authoritative]]

Infine esistono i server DNS [[#^89e8c6|locali]] con cui interagiscono direttamente le applicazioni.

![[Pasted image 20250319082539.png|600]]

>[!note] Root Server
>
>Internet è composto da 13 server DNS radice, dove ognuno è replicato per motivi di sicurezza e affidabilità (in totale diventano 247 root server).
>
>I root server vengono contattati dai server DNS locali per la richiesta di un IP, se il root non lo conosce l
>- contattare un server DNS TLD se non conosce la mappatura
>- ottiene la mappatura
>- restituisce la mappatura al server DNS locale
>  
>![[Screenshot 2025-03-20 at 08.13.57.png|800]]

^6085bc

>[!note] TLD Server
>
>Server TLD (top-level domain): si occupano dei domini `com`, `org`, `net`, `edu`, ecc. e di tutti i domini locali di alto livello, quali `it`, `uk`, `fr`, `ca` e `jp`. Ad esempio:
>- La compagnia Verisign Global Registry Services gestisce i server TLD per il dominio `com`
>- Il Registro.it che ha sede a Pisa all’Istituto di Informatica e Telematica (CNR) gestisce il dominio `it`

^60ff0c

>[!note] Authoritative Server (competenza)
>
>Server di competenza (authoritative server): ogni organizzazione dotata di host Internet pubblicamente accessibili (quali i server web e i server di posta) deve fornire i record DNS di pubblico dominio che mappano i nomi di tali host in indirizzi IP.
>- possono essere mantenuti dall’organizzazione (università) o da un service provider
>- In genere sono due server (primario e secondario)

^1b1857

^7c0b69
>[!note] Local DNS Server
>
>Ciascun ISP (università, società, ISP residenziale) ha un server DNS locale.
>
>Quando un host effettua una richiesta DNS, la query viene inviata al suo server DNS locale che opera da proxy e inoltra la query in una gerarchia di server DNS.
>
>>***oss:*** Non appartiene strettamente alla gerarchia dei server, detto anche “default name server”.

^89e8c6

## Query Iterativa e Ricorsiva

Facciamo 2 esempi uno [[#^b6f9e4|iterativo]] ed un altro [[#^h9j39x|ricorsivo]] di una query dove l’host `cis.poly.edu` cerca l’indirizzo IP di `gaia.cs.umass.edu`.

>[!note] Query Iterativa
>
>![[Screenshot 2025-03-20 at 08.30.17.png|400]]

^b6f9e4

>[!note] Query Ricorsiva
>
>![[Screenshot 2025-03-20 at 08.31.53.png|400]]

^h9j39x

## DNS Caching

Una volta che un server DNS impara la mappatura, la mette nella cache.
- **Durata:** le informazioni nella cache vengono invalidate (spariscono) dopo un certo periodo di tempo (es. 2 giorni).
- **Indirizzi:** tipicamente un server [[#^89e8c6|DNS locale]] memorizza nella cache gli indirizzi IP dei server [[#^60ff0c|TLD]] e di [[#^1b1857|competenza]].

DNS sfrutta il caching per migliorare le prestazioni di ritardo e per ridurre il numero di messaggi DNS che “rimbalzano” in Internet, grazie al caching i nodi radice non vengono visitati spesso.

## DNS Record

Il mapping è mantenuto nei database sotto forma di **resource record (RR)**. 

>[!note] Formato Record
>
>Ogni record ha un formato di questo tipo `(Name, Value, Type, TTL)`, dove:
>- `Name` è la chiave
>- `Value` è il valore
>- `Type` è la tipologia di record
>- `TTL` è il tempo residuo di vita del record

Ogni RR mantiene un mapping, esistono diversi tipi di record in base alla chiave e valore del record:
- [[#^45b2b1|Type A]]
- [[#^72436c|Type CNAME]]
- [[#^7c432a|Type NS]]
- [[#^28b3dd|Type MX]]

>[!example] Esempio Competenze
>
>Il server di [[#^1b1857|competenza]] per un hostname contiene un record di [[#^45b2b1|tipo A]] per l’hostname.
>- Es. `RR (corsi.di.uniroma1.it, 131.111.45.68, A)`
>
>Il server non di competenza per un hostname contiene:
>- un record di [[#^7c432a|tipo NS]] per il dominio che include l’hostname
>- un record di [[#^45b2b1|tipo A]] che fornisce l’indirizzo IP del server DNS nel campo `value` del record NS
>
>Ad esempio un server TLD it non è competente per l’host `corsi.di.uniroma1.it` contiene:
>- `RR (uniroma1.it, dns.uniroma1.it, NS)`
>- `RR (dns.uniroma1.it, 128.119.40.111, A)`

>[!note] Type CNAME
>
>```
>Alias -> Canonical Name
>```
>
>- **name** è il nome alias di qualche hostname "canonico"
>- **value** è l'hostname "canonico"
>- **type** è `CNAME`
>
>```
>Esempio: RR: (foo.com, relay1.bar.foo.com, CNAME)
>```

^45b2b1

>[!note] Type A
>
>```
>Hostname -> IP address
>```
>
>- **name** è il nome dell’host
>- **value** è l’indirizzo IP
>- **type** è `A` che sta per address
>
>```
>Esempio: RR: (relay1.bar.foo.com, 45.37.93.126, A)
>```

^72436c

>[!note] Type NS
>
>```
>Domain name -> Name Server
>```
>
>- **name** è il dominio (ad esempio foo.com)
>- **value** è il nome dell’host del server di competenza di questo dominio
>- **type** è `NS` che sta per Name Server
>
>```
>Esempio: RR: (foo.com, dns.foo.com, NS)
>```

^7c432a

>[!note] Type MX
>
>```
>Alias -> mail server canonical name
>```
>
>- **name** è un Alice
>- **value** è il nome canonico del server di posta associato a *name*
>- **type** è `MX` che sta per Mail e poi non so onestamente
>  
>```
>Esempio: RR: (foo.com, mail.bar.foo.com, MX)
>```

^28b3dd

>[!warning] Altri Record
>
>![[Pasted image 20250320105744.png|700]]

## Messaggi DNS

I record vengono spediti tra server e all’host richiedente all’interno di messaggi DNS, dove un messaggio può contenere più record. Nel protocollo DNS le **domande** (query) e i messaggi di **risposta** hanno entrambi lo stesso formato:

![[Screenshot 2025-03-20 at 11.31.46.png|950]]

>[!note] Approfondimento
>- **Identificazione**: numero di 16 bit per identificare una domanda. la risposta usa lo stesso numero identificatore della domanda.
>- **Flag:** 
>	-  domanda o risposta
>	- richiesta di ricorsione
>	- ricorsione disponibile
>	- risposta di competenza (il server è competente per il nome richiesto)
>- **Numero di:** numero di occorrenze delle quattro sezioni di tipo dati che seguono

>[!note] UDP
>
>I messaggi DNS sono inviati utilizzando il [[Introduzione allo stack protocollare TCP-IP#^ad5398|protocollo UDP]] questo perché:
>- Messaggi corti
>- Tempo per set-up connessione di TCP lungo
>- Un unico messaggio deve essere scambiato tra una coppia di server (nella risoluzione contattati diversi server—se si usasse TCP ogni volta dovremmo mettere su la connessione!!)
>
>Se un messaggio non ha risposta entro un timeout?
>- Semplicemente viene ri-inviato dal resolver (problema risolto dallo strato applicativo)

## Inserimento Record nel Database

Abbiamo appena avviato la nuova società “Network Stud” ora vogliamo avviare un sito web.

Registriamo il nome `networkstud.it` presso registrar (www.registro.it).

Inseriamo nel server di competenza (es. un nostro dns server `dns1.networkstud.it`) un record tipo A per `www.networkstud.it` un record tipo MX per `networkstud.it` ad esempio:
- **A Record:** `www.networkstud.it` → `150.160.15.12` (indirizzo del server web)
- **MX Record:** `networkstud.it` → `mail.networkstud.it` (posta elettronica)
- **CNAME Record:** `mail.networkstud.it` → `mail.google.com` (se usiamo Gmail)

Forniamo al registrar i nomi e gli indirizzi IP dei server DNS di competenza (primario e secondario):
- Il *Registrar* inserisce due RR nel server TLD it: `(networkstud.it, dns1.networkstud.it, NS)` e `(dns1.networkstud.it, 212.212.212.1, A)`

