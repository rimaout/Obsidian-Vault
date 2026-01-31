---
type: Uni Note
class: "[[Basi di Dati 2 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-04-08T10:52
updated: 2026-01-31T13:32
---
## Introduzione

I protocolli di trasporto forniscono la comunicazione logica tra processi applicativi di host differenti, ovvero gli host eseguono i processi come se fossero direttamente connessi. 

I protocolli di trasporto vengono eseguiti nei sistemi terminali e funzionano con un meccanismo di **incapsulamento** quando si invia un messaggio e **decapsulamento** quando si riceve.

A livello di rete abbiamo una comunicazione tra host basata sui servizi del livello di collegamento mentre a livello di trasporto una comunicazione tra processi basata sui servizi del livello di rete.

![[Pasted image 20250408090910.png|600]]

## Indirizzamento

La maggior parte dei sistemi operativi è multi-utente e multi-processo:
- Diversi processi client attivi (host locale)
- Diversi processi server attivi (host remoto)

Per stabilire una comunicazione tra i due processi è necessario un metodo per individuare:
- Host locale
- Host remoto
- Processo locale
- Processo remoto

>[!warning] Porta vs IP e Socket Address
>
>- Ad un *host* è associato un **indirizzo IP**.
>- Ad un *processo* è associata una **porta**.
>  
>La combinazione di indirizzo IP + porta prende il nome di **socket address**.

## Incapsulamento e Decapsulamento

![[Pasted image 20250407222838.png|700]]

Prima di venire spediti i messaggi vengono *incapsulati* ovvero viene *aggiunto un header* che verrà poi riconosciuto quando arriva a destinazione per poi essere de-capsulato per ottenere il messaggio senza header.

Questi pacchetti si chiamano:
- **segmenti** se usiamo ***TCP***
- **datagrammi** utente se usiamo ***UDP***

Questi processi se visti più nello specifico prendono il nome di [[#^3886db|Multiplexing]] e [[#^a89c62|Demultiplexing]]

![[Pasted image 20250408093827.png|500]]

>[!note] Multiplexing
>Il multiplexing avviene nell'host mittente, dove raccoglie i dati da vari socket e li incapsula con l’intestazione corrispondente che verrà poi usata per il demultiplexing.
>
>Ad esempio se in un host abbiamo due processi uno FTP e uno HTTP l’host dovrà raccogliere i dati da questi socket e passarli al livello di rete.

^3886db

>[!note] Demultiplexing
>
>Il demultiplexing avviene nell'host ricevente, e si occupa di **consegnare** i *segmenti/datagrammi* ricevuti alla socket appropriata. Le socket a cui consegnare i dati in input sono determinate attraverso le informazioni contenute negli header.
>
>Come funziona nello specifico il demultiplexing?
>
>- L’host riceve i datagrammi IP, ognuno di questi ha un indirizzo IP di origine e di destinazione
>- Ogni datagramma trasporta un segmento a livello di trasporto
>- Ogni segmento ha un numero di porta per origine e uno per destinazione
>  
>I pacchetti UDP e TCP sono strutturati nel seguente modo:
>
>![[Pasted image 20250408094554.png|400]]

^a89c62
## Socket

Le socket sono delle astrazioni create ed utilizzate dai programmi applicativi per attuare la comunicazione tra un processo client e un processo server.

Una socket é una struttura dati che nella sua forma più semplice è composta da due informazioni un *indirizzo IP* e un *numero di porta* ed è chiamata ufficialmente **Socket Address** .

![[Pasted image 20250320142951.png|800]]

>[!note] Indirizzo IP
>
>Un indirizzo IP permette di identificare un host in una rete, per maggiori informazioni vedi [[DNS#Indirizzi IP]].

>[!note] Numero di Porta
>
>ll numero di una porta non è altro che un **indirizzo di 16 bit** che quindi permette di generare 65535 numeri diversi.
>
>Di tutte queste porte disponibili l'IANA (Internet Assigned Numbers Authority) ha riservato:
>- `0` non usato
>- `1-255` reserved for well known processes
>- `256-1023` reserved for other processes
>- `1024-65535` dedicated to user apps

### Individuare un Socket

 L’interazione tra client e server è bidirezionale, è necessaria quindi una coppia di indirizzi socket **locale** (mittente) e **remoto** (destinatario).

>***oss:*** L’indirizzo locale in una direzione è l’indirizzo remoto nell’altra direzione.

>[!note] Lato Client
>
>Il client ha bisogno di socket address locale (client) e remoto (server):
>
>Il **socket address locale** (client) è fornito dal *sistema operativo* quest'ultimo infatti conosce:
>- l’*indirizzo IP* del computer sul quale il client è in esecuzione 
>- il *numero di porta* assegnato al processo.
>
>Per **socket address remoto** (server):
>- l’*indirizzo IP* viene fornito dal DNS
> - Il *numero di porta* varia in base all’applicazione che stiamo usando (es. http porta 80).

>[!note] Lato server
>
>Il server ha bisogno di un socket address locale (server) e uno remoto (client) per comunicare:
>
>Il **socket address locale** (server) è fornito dal _sistema operativo_ quest'ultimo infatti conosce:
>- l’_indirizzo IP_ è fornito dal sistema operativo su cui il server è in esecuzione
>- il _numero di porta_ è noto al server perché assegnato dal progettista (numero well known o scelto).
>  
>Il **socket address remoto** (client) non è determinato dal server ma semplicemente è il socket address locale del client che si connette, che è comunicato all’interno del pacchetto di richiesta.
>
>>***oss:*** l socket address locale di un server non cambia (è fissato e rimane invariato), mentre il socket address remoto varia ad ogni interazione con client diversi (anche con stesso client su connessioni diverse).

## Servizi di trasporto

Esistono due principali protocolli di trasporto
- [[Protocollo UDP (User Datagram Protocol)]]
- [[Introduzione ai Meccanismi del Protocollo TCP]]

>[!note] Utilizzi dei protocolli nel mondo reale
>
>| Applicazione               | Protocollo a livello applicazione  | Protocollo di trasporto sottostante |
>| -------------------------- | ---------------------------------- | ----------------------------------- |
>| Posta elettronica          | SMTP (RFC 28211)                   | TCP                                 |
>| Accesso a terminali remoti | Telnet (RFC 854)                   | TCP                                 |
>| Web                        | HTTP (RFC 2616)                    | TCP                                 |
>| Trasferimento file         | FTP (RFC 959)                      | TCP                                 |
>| Multimedia in streaming    | HTTP (es. YouTube)                 | TCP o UDP                           |
>| Telefonia Internet         | SIP, RTP, proprietario (es. Skype) | Tipicamente UDP                     |
