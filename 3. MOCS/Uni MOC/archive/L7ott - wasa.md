---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2025-10-07T14:14
updated: 2025-10-07T16:07
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
Ecco gli appunti scritti con la stessa struttura di quelli che mi avevi inviato inizialmente:

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

	## CURL