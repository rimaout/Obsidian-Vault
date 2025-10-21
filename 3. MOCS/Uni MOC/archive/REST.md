---
type: Uni Note
class:
  - "[[WASA (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-10-15T11:25
updated: 2025-10-15T14:17
---
## Cos'è?

**REST** sta per **Representational State Transfer** ed uno *stile* architetturale per sistemi *ipermediali* *distribuiti*. Il suo ***obbiettivo*** è *trasferire la rappresentavano delle [[#^cdde64|risorse]]* da una componente (es. il server) a un altro (es. il client).

>[!note] Risorsa
>
>Una risorsa è qualsiasi informazione che possa essere nominata: un documento, un'immagine, un servizio, un oggetto non virtuale (es. una persona) o una collezione di altre risorse.
>
>- Gli *elementi/valori* di una risorsa possono **variare nel tempo**
>- *Due risorse* possono mappare agli **stessi valori** in un dato momento (Esempio: "versione v2.1" di un programma e "ultima versione" dello stesso programma).

^cdde64

>[!note] Rappresentazione di una risorsa
>
>La rappresentazione della risorsa è lo **stato attuale** o previsto di una risorsa, ovvero il **valore** della risorsa in un momento particolare.
>- ﻿﻿I componenti REST (client o server) eseguono azioni su una risorsa utilizzando una rappresentazione.
>- ﻿﻿La rappresentazione è composta da *dati* e *metadata*. 
>- Il formato dei dati è noto come "*media type*"

>[!note] Identificatori di Risorsa (URI)
>
>Gli identificatori sono usati per identificare, ovvero indirizzare, una risorsa.
>
>Una ***Uniform Resource Identifier (URI)*** è una *sequenza unica* di caratteri che *identifica* una risorsa logica o fisica (Esempio: `http://example.com/users`).
>
>>**URI Best Practice:** Utilizzare ***sostantivi*** per indicare le risorse
>>- ***singolari*** per risorse singole
>>- ***plurali*** per risorse multiple
>  
>>**URI Notation:** 
>>1. Forward slash (`/`): Usato per esprimere la gerarchia
>>	- *﻿﻿﻿Suggerimento*: usare il *trailing slash* solo se la risorsa non è una *foglia*
>>2. ﻿﻿﻿Preferire i trattini (`-`) agli underscore (`_`)
>>3. ﻿﻿﻿Utilizzare solo lettere minuscole
>>4. ﻿﻿﻿Non utilizzare estensioni di file (il media type è comunicato negli header)
>>5. ﻿﻿﻿Utilizzare la **componente query** per filtrare (Esempio: `http://example.com/managed-devices/?region=USA`)
>
>| Regola | Esempio Positivo | Esempio Negativo |
>|---|---|---|
>| Risorsa Singola (Singolare) | `/users/45`| `/get-user/45` (Contiene un verbo) |
>| Collezione (Plurale) | `/invoices` | `/invoice-list` |
>| Gerarchia | `/users/45/orders` |`orders-from-user/45` |
>| Separazione | Preferire i trattini (`-`) | Evitare gli underscore(`_`)| 
>| Media Type | Jon usare estensioni (es. . json) | `/products/123.json` |

>[!note] Operazioni sulle URI
>
>Le `URI` non vengono utilizzate per definire delle operazioni, ad esempio sono errori:
>- `http://example.com/get-managed-devices/{id}`
>- `http://example.com/add-managed-devices/{id}`
>
>Le URI sono usate per *identificare* in modo univoco le risorse e non le azioni su di esse.
>﻿﻿
>﻿﻿Azioni diverse possono essere eseguite su una risorsa attraverso i metodi supportati (`GET`, `PUT`, e `DELETE` ...), un esempio di URI corretta su cui effettuare delle operazioni è `http://example.com/managed-devices/{id}`.

## Restful System Constraints

I vincoli di un sistema RESTful sono:
1. ﻿﻿﻿client-server
2. ﻿﻿﻿stateless
3. ﻿﻿﻿cacheable
4. ﻿﻿﻿uniform-interface
5. ﻿﻿﻿layered system

>[!note] Client-Server
>
>Applica la separazione delle responsabilità infatti:
>- il client gestisce l'UI
>- il server gestisce l'archiviazione dei dati
>
>Questo migliora la **portabilità**, la **scalabilità**

>[!note] Stateless
>
>Ogni richiesta del **client** deve *contenere* tutte le *informazioni necessarie* per essere compresa
>- Non può sfruttare alcun contesto memorizzato sul server
>- Lo stato della sessione è mantenuto sul client (lo stato sella risorsa è mantenuto sul server)

>[!note] Cacheable
>
>Il client può riutilizzare una rappresentazione della risorsa (dati) che è considerata cacheable.
>- Il periodo di tempo per tui la risorsa può essere messa in cache è specificato nella risposta.

>[!note] Uniform-Interface 🟠 (non ho ben capito)
>
>Un'interfaccia uniforme tra i componenti promuove la standardizzazione (a discapito dell'efficienza). ﻿﻿Le implementazioni sono disaccoppiate dai servizi che forniscono.
>
>﻿﻿I quattro vincoli dell'interfaccia sono:
>- ﻿﻿Identificazione delle risorse
>- Manipolazione delle risorse tramite rappresentazioni
>- ﻿﻿Messaggi auto-descrittivi
>- ﻿﻿Hypermedia come motore dello stato dell'applicazione (il client necessita solo della URI iniziale)
>  
>**Esempio:** API REST basate su HTTP usano metodi standard (`GET`, `POST`, `PUT`, `DELETE`, etc.) e gli URI per identificare le risorse.

>[!note] Layered System
>
>Nella *comunicazione* possono essere *coinvolti diversi componenti* in un'architettura a strati (ad esempio: origin server, gateway, proxy, user agent).
>- ﻿﻿I componenti intermedi agiscono sia come client che come server; inoltrano richieste e risposte, a volte con una traduzione
>- ﻿﻿Ogni componente non può "vedere" oltre lo strato immediatamente adiacente con cui interagisce

## HTTP vs. REST

In un'architettura RESTful, i metodi HTTP (noti come "Verbi") definiscono l'azione che si desidera eseguire sulla Risorsa (URI).

Quindi gli URI identificano la cosa, i metodi HTTP definiscono cosa fare con quella cosa.

| Metodo | Funzione                                         | Corrispondenza |
| ------ | ------------------------------------------------ | -------------- |
| GET    | Recupera una risorsa o una collezione.           | Read           |
| POST   | Crea una nuova risorsa in una collezione.        | Create         |
| PUT    | Sostituisce completamente una risorsa esistente. | Update/Replace |
| DELETE | Rimuove una risorsa specifica.                   | Delete         |
| PATCH  | Applica modifiche parziali a una risorsa.        | Update/Modify  |

### Esempi di azioni corrette

>[!note] Ottenere Dati
>- *Obiettivo:* Ottenere tutti i prodotti in vendita.
>- *﻿﻿Design corretto:* `GET /products`
>- *﻿﻿Motivazione:* Si sta recuperando la collezione di prodotti.

>[!note] Creare una nuovo risorsa
>
>- *Obiettivo:* Aggiungere un nuovo utente.
>- ﻿﻿*Design corretto:* `POST /users` (corpo della richiesta contiene i dati del nuovo utente)
>- ﻿﻿*Risposta attesa:* `201 Created`, l'API dovrebbe restituire la nuova risorsa e l'URI per accedervi

>[!note] Eseguire una funzione specifica
>
>Se un azione non è mappabile a CRUD (es. "pubblica documento" o "Cambia password"), ci sono due approcci accettati:
>
>>**1. Modeling come Risorsa:** ovvero modellare l'azione come una risposta:
>> - *Esempio:* `POST /documents/{id}/publish` (publicare un documento)
>
>>**2. PATCH (modifica stato):** ovvero utilizzare `PATCH` per aggiornare un attributo di stato
>>- *Esempio:* `PATCH /documents/{id}` con corpo: `{status: "published"}`
>
>Il secondo approccio (`PATCH`)  è preferito perché mantiene un modello più puro, in cui si agisce sullo *stato* della risorsa.
