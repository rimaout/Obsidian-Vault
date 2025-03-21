---
type: Uni Note
class: "[[Reti (class)]]"
academic year: 2024/2025
related:
  - "[[Introduzione Livello Applicazione (TCP-IP)]]"
completed: true
created: 2025-03-18T09:29
updated: 2025-03-18T10:05
---
## Introduzione 

Il Web Caching consiste nel salvare le pagine richieste per riutilizzarle in seguito senza doverle richiedere al server.

>[!note] Prestazioni
>
>Questo strumento permette di migliorare le prestazioni sia client che del server infatti:
>- Il client non dovrà aspettare le risposte del server.
>- Il server riceve meno richieste riducendo il carico

Il caching può essere eseguito da [[#Browser Caching|Browser]] o attraverso un [[#Proxy Caching|Proxy]].
## Browser Caching

In questo caso è browser a mantenere una cache delle pagine visitate

>[!note] Funzionalità
>
>Esistono vari meccanismi per la gestione della cache locale:
>
>- L’utente può impostare il numero di giorni dopo i quali i contenuti della cache vengono cancellati.
>- La pagina può essere mantenuta in cache in base alla sua ultima modifica (es. modificata un’ora prima -> mantenuta per un’ora, oppure un giorno, un mese, etc.)
>- Si possono utilizzare informazioni nei campi intestazione dei messaggi per gestire la cache
>	• Es: campo Expires specifica la scadenza dopo la quale la pagina è considerata obsoleta (stale)
>	• Non sempre rispettato dai browser

## Proxy Caching

Si inserisce un sever proxy tra la comunicazione del client ed il server originale. Questo server proxy mantiene delle pagine visitate.

Il browser trasmette tutte le richieste HTTP alla cache dove:
- se l'oggetto è presente nella cache allora verrà fornito al client dalla cache
- altrimenti la cache richiede l’oggetto al server d’origine e poi lo inoltra al client

>***oss:*** La cache opera come client (fa richieste al server originale) e come server (risponde al client).

![[Pasted image 20250317185850.png|450]]

>[!note] Server Proxy in una LAN
>
>![[Pasted image 20250317190137.png|600]]
>
>Tipicamente la cache è installata da un ISP (università, aziende o ISP residenziali

>[!done] Vantaggi
>- Riduce i tempi di risposta alle richieste dei client.
>- Riduce il traffico sul collegamento di accesso a Internet.
>- Internet arricchita di cache consente ai provider meno efficienti di fornire dati con efficacia.

## Inserimento e Validazione di un oggetto

>[!note] Inserimento
>1. Il **Client** invia messaggio di richiesta HTTP alla cache:
>	- `GET /page/figure.gif`
>	- `Host: www.sito.com`
>1. La **cache** non ha l’oggetto e quindi inoltra la richiesta HTTP al **Server**.
>2. l **server** invia risposta HTTP alla cache:
>	- `HTTP/1.1 200 OK`
>	- `Date: …`
>	- `Last-Modified: Wed, 2 Jul 2008 09:23:24`
>	- `(dati dati dati …)`
>1. La **cache** memorizza la pagina per richieste future, mantenendo la data di ultima modifica.
>2. La cache invia la risposta al client.

>[!note] Validazione
>
>1. Il **Client** invia messaggio di richiesta HTTP alla cache:
>	- `GET /page/figure.gif`
>	- `Host: www.sito.com`
>2. La **cache** ha l’oggetto, ma prima di inviarlo al client deve verificare che non sia **scaduto** (modificato sul server di origine).
>3. La cache esegue una richiesta verso il Web server che mantiene l’oggetto, per verificarne la validità mediante il metodo [[#^6f68a1|Get Condizionale]].
>- nel metodo GET Include una riga di intestazione `If-Modified-Since- <data>`

>[!warning] Get Condizionale
>
>![[Pasted image 20250318100446.png|800]]

^6f68a1

## Esempio

Immaginiamo avere una rete LAN collegata ad Internet attraverso un collegamento di accesso, con queste caratteristiche:
- Collegamento LAN - Internet: `15 Mbps`
- Rate interno alla Lan: `100 Mbps`

![[Pasted image 20250318093945.png|500]]

Facciamo queste ipotesi:
- Dimensione media di un oggetto: `1 Mb`
- Frequenza media di richieste al server d’origine: `15 richieste al secondo`
- Ritardo per recuperare un oggetto sulla rete internet (Internet delay): `2 sec`
- Il tempo totale di risposta (total delay): `LAN delay + access delay + Internet delay`

Facciamo dei calcoli:
- [[Capacità e Prestazioni di una Rete#^1e0e6b|Intensità di traffico]]  (`La/R`) sulla LAN: `(15req/s*1Mb/req)/100Mbps = 15%`  corrisponde ad un ritardo nel ordine delle decine di `ms`.
- [[Capacità e Prestazioni di una Rete#^1e0e6b|Intensità di traffico]]  (`La/R`) sul collegamento con d'accesso: `(15req/s*1Mb)/15Mbps = 100%` corrisponde ad un ritardo nel ordine di minuti.

Visto che `ritardo totale = ritardo di Internet + ritardo di accesso + ritardo della LAN` il ritardo per ogni richiesta ad Internet sarà nel ordine di minuti e non va bene.

Per risolvere questo problema abbiamo due metodi:
1. [[#^430d94|Aumentare ampiezza di banda del collegamento]]
2. [[#^bd41c9|Installare una cache]]

>[!note] Aumentare ampiezza di banda del collegamento
>
>Aumentare l’ampiezza di banda del collegamento d’accesso a 100 Mbps.
>
>**Risultati:**
>
>- [[Capacità e Prestazioni di una Rete#^1e0e6b|Intensità di traffico]] sulla LAN con d'accesso: `15%`
>- [[Capacità e Prestazioni di una Rete#^1e0e6b|Intensità di traffico]] sul collegamento con d'accesso: `15%`
>- Ritardo totale = `ritardo di Internet + ritardo di accesso + ritardo della LAN = 2 sec + msecs + msecs`
>
>Abbiamo risolta i problema ma questa soluzione non sempre attuabile e comunque costoso aggiornare il collegamento.

^430d94

>[!note] Installare una cache
>
>Installiamo una cache nella rete LAN, supponiamo che quest ultima abbia un hit rate pari a `0.4`.
>
>**Conseguenze:**
>- il 40% delle richieste sarà soddisfatto quasi immediatamente (circa `10ms`) dalla cache.
>- il restante 60% delle richieste sarà soddisfatto dal server d’origine.
>  
>**Risultati:** Ritardo totale medio = ritardo di Internet + ritardo di accesso + ritardo della LAN = `0,6*(2,01) sec + 0.4*(0.01) sec ~ 1,2 sec`.

^bd41c9