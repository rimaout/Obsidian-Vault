---
type: Uni Note
class:
  - "[[WASA (class)]]"
academic year: 2024/2025
related:
completed: false
created: 2026-09-10T20:14
updated: 2026-09-15T00:03
---
## Docker

>[!note] Cos’è Docker e quale problema risolve? 🟠

>[!note] Differenza tra container e macchina virtuale? 🟠

>[!note]- Cos’è un Dockerfile e come funziona? 🟢 
>
>Un Dockerfile è un file contenente le istruzioni per la creazione di un'immagine Docker.
>
>Le operazione principali sono:
>- `FROM`: Definisce l'immagine di base (`debian` or `go`)
>- `WORKDIR`: Imposta la directory di lavoro interna al container per i comandi successivi
>- `COPY`: Copia file e codice sorgente dal sistema host all'interno dell'immagine
>- `RUN`: Esegue comandi durante la fase di build per installare dipendenze o compilare l'applicazione
>- `CMD`: Specifica il comando predefinito da eseguire unicamente all'avvio del container, solitamente utilizzato per eseguire il binario
>  
>Docker costruisce l'immagine, eseguendo in modo sequenziale le istruzioni del Dockerfile attraverso il Docker Daemon:
>- **Creazione dei Layer**: Ogni istruzione (`RUN`, `COPY`) crea un container temporaneo, applica le modifiche e le salva come uno _layer_ immutabile in sola lettura
>- **Distinzione tra Immagine e Container**: L'immagine finale è composta esclusivamente da questi layer immutabili sovrapposti. Il layer scrivibile (_container layer_) non appartiene all'immagine: viene aggiunto sopra di essa solo al momento dell'avvio con `docker run`.
>  
>**Multi-Stage Build**, che usano più istruzioni `FROM` nello stesso Dockerfile per separare la fase di compilazione da quella di esecuzione, copiando nell'immagine finale solo gli artefatti necessari.

>[!note] Cos’è Docker Compose e perché si usa? 🟠

>[!note]- Architettura Docker? 🟢
>
>Docker segue un'architettura client-server composta da tre elementi pricipali: 
>- docker client : è una interfaccia (cli o app) con cui l'utente interagisce con docker deamon
>- docker daemon : è il motore di docker che costruisce le immagini , esegue il container, gestisce la rete
>- docker registry : è il luogo dove sono salvate le immagini docker come docker hub

>[!note]- Come comunicano i servizi tra loro? 🟢
>
>Solitamente se si hanno più container che verranno eseguiti allora Docker Compose comunicano tramite una rete interna creata automaticamente. Ogni servizio è raggiungibile tramite il proprio nome, che funge da hostname DNS. Ad esempio il frontend può chiamare il backend usando ‘api-server:3000’ invece di localhost.
>
>---
>
>Ma nel nostro caso nel file `webui/vite.config.js` è presente `__API_URL__: "http://localhost:3000"` quindi il front end utilizzerà questo indirizzo per comunicare con il backend.

## API

>[!note]- Metodi HTTP 🟢
>
>Le operazioni HTTP hanno queste 3 caratteristiche:
>- **Idempotenza**: utilizzarla la stessa identica richiesta una o più volte sullo produce sempre lo stesso risultato
>- **Safe** : non modifica lo stato del server.
>- **Cacheable** : la risposta può essere memorizzata e riutilizzata
>
>| Metodo | Cosa fa | Idempotente | Safe | Cacheable |
>| --- | --- | --- | --- | --- |
>| GET | Richiesta dati | ✅ | ✅ | ✅ |
>| POST | Creare una risorsa | ❌ | ❌ | ❌ |
>| PUT | Sostituzione di una risorsa | ✅ | ❌ | ❌ |
>| PATCH | Aggiornamento parziale | ❌ | ❌ | ❌ |
>| DELETE | Eliminazione di una risorsa | ✅ | ❌ | ❌ |
>
>>[!warning] Differenza tra POST e PUT
>>
>>La principale differenza tra POST e PUT è l'effetto sulla risorsa:
>>
>>- **POST**: crea un nuovo subordinato della risorsa specificata nell'URI. Se si esegue la stessa richiesta POST più volte, si creano più subordinati, anche se con lo stesso contenuto. Questo significa che POST non è idempotente.
>>- **PUT**: sostituisce la risorsa specificata nell'URI, se esiste, o la crea se non esiste. Se si esegue la stessa richiesta PUT più volte con lo stesso contenuto, la risorsa viene sostituita o creata solo una volta, quindi PUT è idempotente.

>[!note]- HTTP Response Status Codes? 🟢
>
>Categorie di errori:
>- **`2xx` - Success**: La richiesta è stata ricevuta, compresa e accettata con successo.
>- **`4xx` - Client Errors**: La richiesta è sintatticamente errata o non può essere soddisfatta.
>- **`5xx` - Server Errors**: Il server ha riscontrato un errore interno e non è in grado di completare la richiesta
>
>| Codice | Nome | Significato | 
>| --- | --- | --- |
>| 200 | OK | Richiesta completata con successo |
>| 201 | Created | Risorsa Creata (POST) |
>| 204 | No Content | Successo senza corpo di risposta |
>| 400 | Bad Request | Richiesta non valida (errore client) |
>| 401 | Unauthorized | Utente non autenticato |
>| 403 | Forbidden | Utente non autorizzato |
>| 404 | Not Found | Risorsa non trovata |
>| 500 | Internal Server Error | Errore generico del server |
>| 502 | Bad Gateway | Errore tra client e server |
>| 503 | Service Unavailable | Server non disponibile |

>[!note]- Cos'è un' API RESTful e quali sono i suoi principi? 🟢
>
>REST (Representational State Transfer) è uno stile architetturale per sistemi distribuiti che definisce come far comunicare client e serve, utilizzando il protocollo HTTP per lo scambio dello stato delle risorse. 
>
>Un'API è definita _RESTful_ quando rispetta i vincoli fondamentali dell'architettura:
>- **Client-Server**: Netta separazione tra l'interfaccia utente e la logica dati backend.
>- **Stateless**: Il server non memorizza lo stato delle sessioni. Ogni singola richiesta dal client deve contenere tutte le informazioni (compresi i token di autenticazione) necessarie all'elaborazione.
>- **Cacheable**: Le risposte del server devono indicare se e per quanto tempo possono essere memorizzate in cache.
>- **Layered System**: L'architettura può comprendere livelli intermedi (proxy, bilanciatori di carico, API Gateway) in modo del tutto trasparente per il client.
>- **Uniform Interface**: utilizzo degli URI (uniform resource identifier), operazioni e codici di stato HTTP.

>[!note]- OpenAPI: cos’è e a cosa serve? 🟢
>
>**OpenAPI** è uno standard  per descrivere API in modo sia _human-readable_ che _machine-readable_ tramite un file **YAML**.
>
>Obbiettivo definire il contratto/interfaccia tra chi sviluppa il backend e chi consuma le API (front end), contiene gli endpoint e i relativi metodi HTTP.
>
>Per ogni combinazione di endpoint e metodo sono definite la la modalità di autenticazione,  struttura della richiesta e tutte le possibili risposte.
>
>Permette uno sviluppo API-First: Permette a frontend e backend di concordare l'interfaccia prima di scrivere il codice. Una volta approvato il contratto, le due parti posso essere sviluppate in modo indipendente.

>[!note]- Differenza tra SOP e CORS? 🟢
>
>La **SOP (Same-Origin Policy)** è una politica di sicurezza applicata direttamente dal browser che impedisce a uno script caricato da un'origine (es. `https://frontend.com`) di leggere le risposte provenienti da un'altra origine (es. `https://backend.com`). Serve a proteggere l'utente, evitando che siti malevoli possano sottrarre o accedere a dati sensibili.
>
>Tuttavia, la SOP imporrebbe un'architettura centralizzata su una singola origine. Nei servizi moderni è normale avere un'architettura disaccoppiata: ad esempio, nel nostro progetto il frontend risiede su `localhost:8080` e il backend su `localhost:3000`, che costituiscono due origini differenti per via della porta.
>
>Per permettere questa comunicazione in modo controllato si usa il **CORS (Cross-Origin Resource Sharing)**: un meccanismo con cui il backend comunica al browser quali origini esterne sono autorizzate ad accedere alle sue risorse.
>
>>[!warning] Definizione Origine
>>Due URL condividono la stessa origine solo se coincidono tutti e tre i seguenti elementi: **Protocollo**, **Dominio** e **Porta**.

## JavaScript

>[!note]- Cos’è una Promise in JavaScript? 🟢
>
>Una Promise è un oggetto che rappresenta il risultato futuro di un’operazione asincrona. Può trovarsi in uno di tre stati: 
>- **pending** (in corso)
>- **fulfilled** (completata con successo)
>- **rejected** (fallita)
>    
>Il risultato si gestisce con i metodi `.then()` e `.catch()` oppure, in modo più moderno, tramite la sintassi `async/await`.

>[!note]- Come funziona l’asincronia in JavaScript? 🟢
>
>JavaScript è _single-threaded_, quindi esegue un'istruzione alla volta sul thread principale. Per non bloccarsi durante operazioni lente (come richieste di rete o timer), delega queste operazioni in background al browser o a Node.js. Quando l'operazione termina, il risultato può essere gestito tramite Promise o `async/await`.

>[!note]- Come si gestiscono gli errori? 🟢
>
>La gestione varia in base alla sintassi scelta:
>- Con `async/await` si utilizzano i classici blocchi `try...catch`. 
>- Con le *Promise tradizionali* si concatena il metodo `.catch()` in fondo alla catena delle `.then()`.
>
>**Approccio classico**: Promise con `.then()` e `.catch()`
>```js
>function ottieniDatiUtente(id) {
  >fetch(`https://api.example.com/users/${id}`)
>    .then((response) => {
>      if (!response.ok) {
>        throw new Error(`Errore HTTP: ${response.status}`);
>      }
>      return response.json(); // Restituisce un'altra Promise
>    })
>    .then((data) => {
>      console.log("Dati ricevuti con successo:", data);
>    })
>    .catch((error) => {
>      // Gestisce qualsiasi errore avvenuto nella catena dei .then()
>      console.error("Si è verificato un errore:", error.message);
>    });
>}
>```
>
>**Approccio moderno:** `async/await` con `try/catch`
>
>```js
>async function ottieniDatiUtente(id) {
>  try {
>    const response = await fetch(`https://api.example.com/users/${id}`);
>    
>    if (!response.ok) {
>      throw new Error(`Errore HTTP: ${response.status}`);
>    }
>    
>    const data = await response.json(); // Attende il riempimento della Promise
>    console.log("Dati ricevuti con successo:", data);
>    
>  } catch (error) {
>    // Intercetta sia gli errori lanciati manualmente che quelli delle Promise respinte
>    console.error("Si è verificato un errore:", error.message);
>  }
>}
>```
>
>>[!warning] Con le Promise tradizionali (Nessun flag nella firma)
>>
>>Nessuna parola chiave avvisa che la funzione è asincrona. È il valore ritornato che fa la differenza:
>>
>>```js
>>// La firma è quella di una normale funzione sincrona
>>function caricaDati() {
>>return new Promise((resolve) => {
>>    setTimeout(() => resolve("Dati caricati"), 1000);
>>  });
>>}
>>```
>>
>>Chi invoca `caricaDati()` sa che è asincrona solo perché leggendo il codice (o la documentazione) vede che il valore di ritorno possiede i metodi `.then()` e `.catch()`.

>[!note] Cos’è il DOM?
>
>Il DOM (Document Object Model) è una struttura ad albero in memoria creata dal browser quando interpreta il codice HTML. Ogni tag, attributo e testo della pagina diventa un "nodo" dell'albero, rendendo l'interfaccia accessibile e manipolabile dinamicamente tramite JavaScript.

>[!note]- Come viene modificato il DOM in Vue.js? 
>
>In Vue.js il DOM reale non viene modificato direttamente in modo imperativo. Vue adotta un approccio **dichiarativo e reattivo** basato su tre pilastri:
>
>- **Sistema di Reattività**: Vue traccia i dati del componente (`ref` / `reactive`). Quando un dato cambia, il framework rileva automaticamente la modifica senza dover scrivere codice manuale per aggiornare l'interfaccia. 
>- **Virtual DOM (VDOM)**: Per ottimizzare le prestazioni, Vue mantiene in memoria una copia sintetica e leggera del DOM reale, detta _Virtual DOM_.
>- **Diffing e Patching**: A ogni variazione di stato, Vue crea un nuovo Virtual DOM e lo confronta con quello precedente (_algoritmo di diffing_). Individuate le differenze, applica al DOM reale esclusivamente i nodi che sono stati modificati (_patching_), evitando di ri-renderizzare l'intera pagina.

## Go

>[!note] Come si gestiscono gli errori?

>[!note] Differenza tra errore gestito e panic (in Go)?

**Gestione degli errori (`error`)** In Go non esistono le eccezioni tradizionali (`try/catch`). Gli errori previsti o gestibili vengono trattati come **valori** e restituiti come ultimo parametro di ritorno dalle funzioni (interfaccia `error`).

- **Quando si usa**: Per situazioni anomale ma attese durante il normale flusso (es. file non trovato, input utente non valido, timeout di rete).
    
- **Comportamento**: Il programma gestisce l'errore in modo esplicito (`if err != nil`) e continua la sua esecuzione senza interrompersi.
    

**Il Panic (`panic`)** Il `panic` indica una condizione anomala grave dovuta a un bug del programmatore o a un fallimento irreversibile dell'ambiente.

- **Quando si verifica**: Automaticamente dal runtime (es. _nil pointer dereference_, _out-of-bounds_ su uno slice) oppure invocato manualmente dallo sviluppatore tramite la funzione `panic()`.
    
- **Comportamento**: Interrompe immediatamente il normale flusso di esecuzione, risale lo stack delle chiamate eseguendo tutte le funzioni dichiarate con **`defer`** e, se non intercettato, termina il programma stampando il _stack trace_.
    

**Punto chiave per l'orale: Il meccanismo di `recover()`**

Sottolinea al professore che un `panic` **può essere catturato** per evitare il crash dell'applicazione usando la funzione `recover()` all'interno di un blocco `defer`. Questo è fondamentale per servizi backend altamente disponibili (es. server web) che devono isolare il crash di una singola richiesta senza far cadere l'intero server.