---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-04-12T16:50
updated: 2025-04-12T18:45
---
### Esercizio 1

Un client (browser) vuole accedere alla pagina web di un sito: `http://www.example.com/index.html`. Il sito è ospitato su un server web che utilizza il protocollo HTTP/1.1.

**Domanda 1:** Quale richiesta HTTP invierà il browser per ottenere la pagina? Scriver l’header completo della richiesta HTTP che il client invia al server. 

```
GET /index.html HTTP/1.1
- Host: www.example.com
- Accept: text/html
- User-Agent: Mozilla/5.0 (messo a caso)
- Connection: keep-alive (messo a caso)
```

**Domanda 2:** Se la richiesta è corretta e il file `index.html` esiste, quale codice di stato HTTP restituirà il server? Scrivere l’header della risposta HTTP che il server potrebbe inviare.

```
HTTP/1.1. 200 OK
- Data: Sat, 12 Mar 2025 17:11:69 GMT
- Server: Apache/2.4.41 (Ubuntu) (messo a caso)
- Content-Type: text/html
- Content-Length: 3456 (messo a caso)
- Connection: keep-alive (messo a caso)
```

**Domanda 3:** Se la pagina `index.html` non esiste, quale codice di stato restituirà il server?

```
404 
```

**Domanda 4:** Se l’accesso alla pagina è vietato per motivi di autorizzazione, quale codice di stato verrà restituito?

```
403
```

---
### Esercizio 2

Un utente vuole visitare la pagina web `www.example.com` dal
proprio browser. Il processo client web, tuttavia, non conosce
l'indirizzo IP del sito e deve interrogarlo attraverso il sistema DNS.

**Domanda 1:** Quali sono i passi che il computer dell’utente esegue per ottenere l’indirizzo IP di `www.example.com`? e quali server DNS vengono coinvolti nel processo di risoluzione del nome?

Ci sono due modi, ricorsivo ed iterativo.

>[!note] Iterativa
>
>Il client effettua un interrogazione del server DNS locale:
>
>Se l'indirizzo è presente in cache viene inviato direttamente al client
>
>Se non è nella cache allora:
>1. Il DNS local interroga il server root e richiede l'indirizzo del TLD Name Server per .com.
>2. Il server TLD (es. .com) indica al server DNS local il Name Server Autorevole di example.com.
>3. Name Server Autorevole di example.com risponde con l’indirizzo IP.
>4. Il server DNS locale risponde al client col l'indirizzo IP ricevuto dal Name Server Autorevole di example.com
>   
>   ![[Screenshot 2025-03-20 at 08.30.17.png|300]]

>[!note] Ricorsiva
>
>![[Screenshot 2025-03-20 at 08.31.53.png|300]]

---
### Esercizio 3

**Domanda:** Scrivere un esempio di una coppia di resource record che sono memorizzati in un server DNS di tipo radice (spiegare il significato dei campi dei resource record indicati).

```
RR NS: (.com, dns.com, NS)

- .com -> dominio
- dns.com -> nome server
- NS -> tipo RR
```

```
RR A: (dns.com, 157.12.132.8, A)

- dns.com -> nome server
- 157.12.132.8 -> indirizzo IP
- A -> tipo RR
```

---
### Esercizio 4

**Domanda:** Dato il seguente resource record dire se è corretto. Se non è corretto modificarlo per renderlo corretto. Infine spiegarne il tipo specificando anche in quale livello della gerarchia in cui è memorizzato.

```
RR: (uniroma1.it, ns1.garr.net, A)
```

**Risposta:**

Il record dato non è coretto perché per essere un resource record di tipo `A` deve contenere come valore l'indirizzo IP.

Abbiamo due modi per correggerlo:
1. `RR: (uniroma1.it, ns1.garr.net, NS)` -> livello TLD
2. `RR: (127.42.137.7, uniroma1.it, A)` -> livello Server Competenza
