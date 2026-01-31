---
type: Uni Note
class: "[[Reti (class)]]"
academic year: 2024/2025
related:
  - "[[Introduzione Livello Applicazione (TCP-IP)]]"
completed: true
created: 2025-03-17T09:41
updated: 2026-01-31T13:32
---
## Introduzione

**World Wide Web (WWW)** è un applicazione Internet nata dalla necessità di scambio e condivisione di informazioni tra ricercatori universitari di varie nazioni.

>[!note] Caratteristiche
>
>- Opera su richiesta (on demand)
>- Facile rendere informazioni disponibili 
>- Collegamenti ipertestuali (hyperlinks) e motori di ricerca permettono di navigare su una grande quantità di siti

>[!note] Componenti
>
>- *Web client:* interfaccia con l’utente (es. browser)
>- *Web server* (es. Apache)
>- *HTML:* linguaggio standard per pagine web
>- *HTTP:* protocollo per la comunicazione tra client e server Web (indipendente dal linguaggio di programmazione usato)
>
>![[Pasted image 20250313142728.png|600]]

>[!note] Architettura generale di un browser
>
>![[Pasted image 20250317094418.png|500]]

## Terminologia

- Una pagina web è costituita da oggetti
- Un oggetto può essere un file HTML, un’immagine JPEG, un’applet Java, un file audio, ...
- Una pagina web è formata da un file base HTML (HyperText Markup Language) che include diversi oggetti referenziati
- Ogni oggetto è referenziato da un URL (Uniform Resource Locator), ovvero un file che può essere ottenuto attraverso un URL

>[!note] URL
>
>**Uniform Resource Locator** (URL), composto di 3 parti:
>1. Il protocollo
>2. Il nome della macchina in cui è situata la pagina
>3. l percorso del file (localmente alla macchina) che indica la pagina il nome del file e la posizione nel filesystem
>
>**Struttura:**
>- `protocol://host/path` - utilizzato quando la porta è standard (porta standard è 80)
>- `protocol://host:**porta**/path` - utilizzato quando è necessario specificare il numero di porta
>
>![[Pasted image 20250317094651.png|600]]

>[!note] Tipo di Documento
> - **Documento statico** - Contenuto predeterminato memorizzato sul server
>- **Documento dinamico** -  Creato dal web server alla ricezione della richiesta
>- **Documento attivo** - Contiene script o programmi che verranno eseguiti nel browser ovvero lato client (es. applet java)

## HTTP

HTTP sta per **hypertext transfer protocol**, è il protocollo che HTTP definisce il modo in cui i *client web* richiedono pagine ai *server web* e come questi le trasferiscono ai client.

![[Screenshot 2025-03-17 at 09.53.15.png|300]]

>[!note] Lato Client
>1. Il browser determina l’URL ed estrae host e filename
>2. Esegue connessione TCP alla porta 80 dell’host indicato nella URL
>3. Invia richiesta per il file
>4. Riceve il file dal server
>5. Chiude la connessione
>6. Visualizza il file

>[!note] Lato Server
>1. Accetta una connessione TCP da un client
>2. Riceve il nome del file richiesto
>3. Recupera il file dal disco 
>4. Invia il file al client
>5. Rilascia la connessione

## Connessione HTTP

Ci sono 2 principali tecniche di comunicazione tra client e server:

>[!note] Connessione non persistente
>- Un solo oggetto (file http, imagine...) viene trasmesso su una connessione TCP
>- Ciascuna coppia richiesta/risposta viene inviata su una connessione TCP separata
>- Prima di inviare una richiesta al server è necessario stabilire una connessione

>[!note] Connessioni persistenti (attualmente utilizzate)
>- Più oggetti possono essere trasmessi su una singola connessione TCP tra client e server
>- La connessione viene chiusa quando rimane inattiva per un lasso di tempo (timeout) configurabile

>[!warning]  RTT (Round Trip Time)
>
>Il Round Trip Time rappresenta il tempo impiegato da un piccolo pacchetto per andare dal client al server e ritornare al client.
>
>- Le connessioni non persistenti richiedono `2RTT + tempo di trasmissione` per ogni oggetto richiesto dal client. 
>- Nelle connessioni persistenti una volta instaurata la connessione TCP tra client e server questa viene lasciata aperta e quindi ogni oggetto richiede un solo `RTT`.
>
>![[Screenshot 2025-03-17 at 10.10.31.png|300]]
>
>Nelle connessioni persistenti i client mandano richieste sequenziali, nelle connessioni non persistenti invece si possono richiedere più connessioni parallele, questo teoricamente può rendere il trasferimento dei file più veloce ma richiederebbe troppo overhead per la gestione.

### Richiesta HTTP

>[!note] Formato
>
>![[Pasted image 20250313145606.png|450]]
>
>**Esempio:**
>
>![[Pasted image 20250317155459.png|500]]
>
>>***oss:*** `sp` -> space, `cr` -> carriage return, `lf` -> line feed

>[!note] Invio Input Utente
>
> La pagina web spesso include un form per l’input dell’utente esistono due principali modi con cui il client può inviare queste informazioni al server. 
>
>Con il metodo **post** inseriamo le informazioni all'interno del *Entity Body* della richiesta.
>
>Con il metodo **get** inseriamo le informazioni alla fine del *Campo URL*, esempio: `www.somesite.com/animalsearch?monkeys&banana`.

>[!note] Metodi Richieste HTTP
>
>| Metodo | Info |
>| -------- | ---- |
>| **GET** | Usato quando il client vuole scaricare un documento dal server. Il documento richiesto è specificato nell’URL. Il server normalmente risponde con il documento richiesto nel corpo del messaggio di risposta |
>| **HEAD** | Usato quando il client non vuole scaricare il documento ma solo alcune informazioni sul documento (come ad esempio la data dell’ultima modifica). Nella risposta il server non inserisce il documento ma solo degli header informativi. |
>| **POST** | Usato per fornire input al server (contenuto dei campi di un form). L’input arriva al server nel corpo dell’entità. |
>| **PUT** | Utilizzato per memorizzare un documento nel server. Il documento viene fornito nel corpo del messaggio e la posizione di memorizzazione nell’URL. |

^64acb5

>[!note] Intestazione richiesta
>
>![[Pasted image 20250313145315.png|600]]
>
>

### Risposta HTTP

>[!note] Formato
>
>![[Pasted image 20250313145358.png|500]]
>
>**Esempio:**
>
>![[Pasted image 20250317161122.png|600]]

>[!note] Codice di Stato
>
>Quando si effettua una risposta il server comunica dei codici di stato:
>
>| Codice Specifici | Significato |
>| ------- | ---- |
>| **200 OK** | La richiesta ha avuto successo; l’oggetto richiesto viene inviato nel corpo della risposta |
>| **301 Moved Permanently** | L’oggetto richiesto è stato trasferito; la nuova posizione è specificata nell’intestazione `Location` della risposta |
>| **400 Bad Request** | Il messaggio di richiesta non è stato compreso dal server |
>| **404 Not Found** | Il documento richiesto non si trova su questo server |
>| **505 HTTP Version Not Supported** | Il server non ha la versione di protocollo HTTP |
>
>| Codici in Generale | Significato | Esempio |
>| ---------| ---------- | --------- |
>| `1xx` | Information | 100 = server agrees to handle client's request |
>| `2xx` | Success | 200 = request succeeded; 204 = no content present |
>| `3xx` | Redirection | 301 = page moved; 304 = cached page still valid |
>| `4xx` | Client error | 403 = forbidden page; 404 = page not found |
>| `5xx` | Server error | 500 = internal server error; 503 = try again later |

![[Pasted image 20250313145502.png|650]]

#### Esempio

>[!note] Esempio GET
>
>Esempio in cui il client preleva un documento, in particolare viene usando il metodo `GET` per ottenere l'imagine individuata dal percorso `usr/bin/image1`
>
>![[Screenshot 2025-03-17 at 17.15.34.png|550]]
>
>Il messaggio di **richiesta** inviato dal client contiene: 
>- la riga richiesta contiene il metodo (GET), l'URL e la versione (1.1) del protocollo HTTP. 
>- L’intestazione è composta da 2 riche che specificano che i formati imagine (GIF e JPEG) supportati dal client.
>- Il corpo in questo caso è vuoto.
>
>Il messaggio di **risposta** inviato dal server contiene:
>- La riga di stato, che conferma ll successo della richiesta e l'invio del documento.
>- Quattro righe di intestazione che contengono la data, il server, il metodo di codifica del contenuto (la versione MIME, argomento che verrà descritto nel paragrafo dedicato alla posta elettronica) e la lunghezza del documento.
>- Il corpo del messaggio contiene il documento richiesto.

>[!note] Esempio PUT
>
>Esempi in cui il client spedisce al server una pagina Web da pubblicare attraverso il metodo `PUT`.
>
>![[Pasted image 20250317172833.png|550]]
>
>Il messaggio di **richiesta** inviato dal client contiene: 
>- la riga richiesta contiene il metodo (PUT), l'URL e la versione (1.1) del protocollo HTTP. 
>- L’intestazione costituita da 4.
>- Il corpo contiene la pagina Web inviata.
>
>Il messaggio di **risposta** inviato dal server contiene:
>- La riga di stato
>- Quattro righe di intestazione.
>- Il documento creato, un documento CGI, è incluso nel corpo del messaggio di risposta.
