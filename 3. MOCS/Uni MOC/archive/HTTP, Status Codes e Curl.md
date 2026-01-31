---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: true
created: 2025-10-07T14:14
updated: 2026-01-31T13:32
---
## HTTP

HTTP (HyperText Transfer Protocol) è un protocollo di livello applicazione nello stack protocollare id Internet.

È stato inventato nel al CERN nel 1989 ma ancora oggi è in via di sviluppo e aggiornamento (ulima versione è HTTP/3 pubblicata nel 2002)

Questo protocolla è solitamente utilizzato per far comunicare un client con un server o un server con un altro server.

>[!note] Client
>
>**User Agent (UA)** è un qualsiasi programma client che avvia una richiesta (es. browser web, app mobile ...).

>[!note] Server
>
>**Origin Server (O)** è un programma che può originare risposte autorevoli per una data risorsa (es. sito web ...).

A volte tra un l'*User Agent* e l'*Origin Server* possono esserci dei servizi (server) intermediari come i proxy, gateway, tunnel, load balancer, ... .

Un server proxy molto comune è il server cache.

## Metodi HTTP

I metodi più comuni del protocollo HTTP sono:
- GET
- HEAD
- POST
- PUT
- DELETE
- CONNECT
- OPTIONS
- TRACE
- PATCH

Questi metodi possono avere queste tre proprietà:

>[!note] Safe (sicuro)
>
>Un metodo che non ha effetti collaterali sulla risorsa, cioè é "sola lettura".
>
>Può tuttavia cambiare lo stato del server in altri modi (es. log)
>
>>Es: `GET`, `HEAD`, `OPTIONS` e `TRACE`

>[!note] Cashable (memorizzatile nella cache)
>
>Metodi che possono consentire a una cache di archiviare e utilizzare una risposta.
>
>>Es: `GET`, `HEAD` e `POST` in determinate condizioni sono cashable.

>[!note] Idempotent (idempotente)
>
>Richieste identiche multiple con quel metodo hanno lo steso effetto di una singola richiesta.
>
>>Es: `PUT`e `DELETE` 

### Operazioni

>[!note] PUT
>
>```
>PUT /course-descriptions/web-and-software-architecture
>```
>
>- **Crea o sostituisce una risorsa**: Se la risorsa specificata nell'URI non esiste, viene creata. Se esiste già, viene sostituita con la risorsa specificata nel payload.
>
>**Proprietà:**
>- è *idempotente*: Eseguire la stessa richiesta PUT più volte ha lo stesso effetto di eseguirla una volta sola.
>- non è *safe*: La richiesta PUT può modificare lo stato della risorsa.
>- non è *cacheable* per default: La risposta a una richiesta PUT non è cacheabile per default, poiché può contenere informazioni sensibili o essere utilizzata per modificare lo stato della risorsa.

>[!note] GET
>
>```
>GET /course-descriptions/web-and-software-architecture
>```
>
>- Richiede una rappresentazione dello stato di una risorsa.
>
>**Proprietà:**
>- è *safe*: La richiesta GET non modifica lo stato della risorsa.
>- è *cacheable*: La risposta a una richiesta GET può essere memorizzata nella cache di un intermediario, a condizione che siano rispettate specifiche condizioni (ad esempio, la data di scadenza).
>- è *idempotente*: Eseguire la stessa richiesta GET più volte ha lo stesso effetto di eseguirla una volta sola.

>[!note] POST
>
>```
>POST /announcements/
>POST /announcements/{id}/comments/
>POST /users/{id}/email
>```
>
>- Crea o modifica un subordinato della risorsa indicata nell'URI.
>
>**Proprietà:**
>- potrebbe essere *cacheable*: La risposta a una richiesta POST potrebbe essere cacheabile, ma dipende dalle specifiche condizioni.
>- non è *safe*: La richiesta POST può modificare lo stato della risorsa.
>- non è *idempotente*: Eseguire la stessa richiesta POST più volte può avere effetti diversi rispetto a eseguirla una volta sola, poiché può creare o modificare più volte i subordinati.

>[!note] DELETE
>
>```
>DELETE /announcements/{id}
>```
>
>- Elimina una risorsa.
>
>**Proprietà:**
>- non è *safe*: La richiesta DELETE può modificare lo stato della risorsa.
>- è *idempotente*: Eseguire la stessa richiesta DELETE più volte ha lo stesso effetto di eseguirla una volta sola, poiché elimina la risorsa solo se esiste.

>[!warning] Differenza tra POST e PUT
>
>La principale differenza tra POST e PUT è l'effetto sulla risorsa:
>
>*   **POST**: crea un nuovo subordinato della risorsa specificata nell'URI. Se si esegue la stessa richiesta POST più volte, si creano più subordinati, anche se con lo stesso contenuto. Questo significa che POST non è idempotente.
>*   **PUT**: sostituisce la risorsa specificata nell'URI, se esiste, o la crea se non esiste. Se si esegue la stessa richiesta PUT più volte con lo stesso contenuto, la risorsa viene sostituita o creata solo una volta, quindi PUT è idempotente.

### Altri metodi utili

| Metodo    | Descrizione                                                                          |
| --------- | ------------------------------------------------------------------------------------ |
| `HEAD`    | Come `GET`, ma non trasferisce il contenuto della risposta (solo header)             |
| `CONNECT` | Stabilisce un tunnel verso il server identificato dalla risorsa target               |
| `OPTIONS` | Descrive le opzioni di comunicazione per la risorsa target                           |
| `TRACE`   | Esegue un test di loop-back del messaggio lungo il percorso verso la risorsa target. |

## Codici di Stato

Le richieste HTTP contengono sempre uno status code che descrive lo stato della richiesta, ne esistono di 5 categorie:


| Categoria Codice      | Descrizione                                                                                |
| --------------------- | ------------------------------------------------------------------------------------------ |
| `1xx` (Informational) | La richiesta è stata ricevuta, processo in corso (*Hold on*).                              |
| `2xx` (Successful)    | La richiesta è stata ricevuta, compresa e accettata con successo (*Here you go*).          |
| `3xx` (Redirection)   | Sono necessarie ulteriori azioni per completare la richiesta (*Go away*).                  |
| `4xx` (Client Error)  | La richiesta contiene sintassi errata o non può essere soddisfatta (*You fucked up*).      |
| `5xx` (Server Error)  | Il server non è riuscito a soddisfare una richiesta apparentemente valida (*I fucked up*). |
|                       |                                                                                            |

>[!note] 1xx Comuni
>
>| Codice |  Descrizione  |
>| --- | --- |
>|     |     |
 
>[!note] 2xx Comuni
>
>| Codice |  Descrizione  |
>| --- | --- |
>| `200` OK | In una richiesta GET, la risposta conterrà un'entità corrispondente alla risorsa richiesta; in una richiesta POST, la risposta conterrà un'entità che descrive o contiene il risultato dell'azione |
>| `201` Created | La richiesta è stata soddisfatta, risultando nella creazione di una nuova risorsa |
>| `204` No Content | Il server ha elaborato con successo la richiesta e non sta restituendo alcun contenuto |

>[!note] 3xx Comuni
>
>| Codice |  Descrizione  |
>| --- | --- |
>| `301` Moved Permanently | Questa e tutte le richieste future dovrebbero essere indirizzate all'URI fornito |
>| `302` Found | Guarda un'altra URL |

>[!note] 4xx Comuni
>
>| Codice |  Descrizione  |
>| --- | --- |
>| `400` Bad Request | Apparente errore del client |
>| `401` Unauthorized | È richiesta l'autenticazione |
>| `403` Forbidden | La richiesta conteneva dati validi ed è stata compresa dal server, ma l'azione è proibita |
>| `404` Not Found | La risorsa non è stata trovata ma potrebbe essere disponibile in futuro|
>| `405` Method Not Allowed | Il metodo di richiesta non è supportato; ad esempio, una richiesta PUT su una risorsa di sola lettura |

>[!note] 5xx Comuni
>
>| Codice |  Descrizione  |
>| --- | --- |
>| `500` Internal Server Error | Condizione inaspettata riscontrata |
>| `501` Not Implemented | Metodo di richiesta non riconosciuto, oppure il server non ha la capacità di soddisfare la richiesta |
>| `502` Bad Gateway | Un gateway o proxy ha ricevuto una risposta non valida dal server a monte |
>| `503` Service Unavailable | Server sovraccarico o inattivo per manutenzione (temporaneo) |
>| `504` Gateway Timeout | Il server non ha ricevuto una risposta tempestiva dal server a monte |

##  Curl Basics


| Metodo        | Scopo                                                         | Sintassi                                                                                                                          |
| ------------- | ------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| GET (Default) | Scarica il contenuto della risorsa                            | `curl https://swapi.dev/api/people/1/`                                                                                            |
| HEAD          | Richiede solo le intestazioni (Header), non il corpo          | `curl -I https://swapi.dev/api/people/1/`                                                                                         |
| POST          | Invia dati per creare una nuova risorsa                       | `curl -X POST -H "Content-Type: application/json" -d {"title": "Test"} https://jsonplaceholder.typicode.com/posts`                |
| PUT           | Invia dati per sostituire una risorsa esistente (Idempotente) | `curl -X PUT -H "Content-Type: application/json" -d {"id": 1, "title": "New Title"} https://jsonplaceholder.typicode.com/posts/1` |
| DELETE        | Elimina la risorsa                                            | `curl -X DELETE https://jsonplaceholder.typicode.com/posts/1`                                                                     |
| HEADERS       | Visualizza tutte le intestazioni (opzione per GET)            | `curl -i https://swapi.dev/api/people/1/`                                                                                         |


