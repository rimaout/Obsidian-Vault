---
type: Uni Note
class: "[[Reti (class)]]"
academic year: 2024/2025
related:
  - "[[Introduzione Livello Applicazione (TCP-IP)]]"
completed: true
created: 2025-03-17T17:36
updated: 2025-04-11T13:15
---
## Introduzione

Il protocollo [[World Wide Web e HTTP|HTTP]] è detto "senza stato", ovvero il server una volta servito il client non mantiene informazioni sulle richieste fatte. Questo perché implementare protocolli che mantengono lo “stato” sono complessi e dispendioso.

Ci sono molti casi in cui il server ha bisogno di ricordarsi degli utenti, per questo si possono usare i Cookie. Il meccanismo dei Cookie rappresenta un modo per creare una sessione di richieste e risposte HTTP “con stato” (stateful).

## Sessione

La sessione rappresenta un contesto più largo rispetto alla richiesta/risposta. Ci possono essere diversi tipi di sessione in base al tipo di informazioni scambiate e la natura del sito.

>[!note] Caratteristiche
>
>Caratteristiche generali di una sessione:
>
>1. Ogni sessione ha un inizio e una fine.
>2.  Ogni sessione ha un tempo di vita relativamente corto. 
>3. Sia il client che il server possono chiudere la sessione. 
>4. La sessione è **implicita** nello scambio di informazioni di stato.

>[!note] Sessione vs Connessione
>
>Per sessione non si intende connessione persistente, ma una sessione logica creata da richieste e risposte HTTP. Una sessione può essere creata su connessioni persistenti e non persistenti.

## Funzionamento

Il server mantiene tutte le informazioni riguardanti il client su un file e gli assegna un identificatore (cookie) che viene fornito al client. Il cookie inviato al client è un **identificatore di sessione (SID)**.

- Il ***client*** ogni volta che manda una richiesta al server fornisce il suo identificatore (cookie): il browser consulta il file cookie, estrae il numero di cookie per il sito che si vuole visitare e lo inserisce nella richiesta http. 
- Il ***server*** mediante il cookie fornito dal client accede al relativo file e fornisce risposte personalizzate.

>[!example] Esempio
>
>![[Screenshot 2025-03-13 at 15.25.36.png|600]]
>
>Dopo la prima richiesta del client, il server invia un set-cookie per inizializzare il cookie nel client.
>
>Il client utilizzera quelo coockie in ogni risposta/richiesta al server per identificarsi.
>

## Durata di un cookie

Il server può specificare la durata di una sessione inviando al client una intestazione `set-cookie` nel messaggio con:
- `Max-Age = delta-seconds` definisce il tempo di vita in secondi di un cookie.
- `Max-Age = 0` per chiudere la sessione.

## Utilizzi 

I cookie possono essere utilizzati per diversi scopi:
- autorizzazioni
- carta per acquisti
- preferenze dell’utente
- stato della sessione dell’utente (e-mail)

 **Privacy:** i cookie permettono ai siti di imparare molte cose sugli utenti.

## Alternative

Per mantenere lo stato e quindi creare una sessione senza utilizzare i cookie è possibili sfruttare [[World Wide Web e HTTP#^64acb5|metodo POST della richiesta HTTP]].

Il client mantiene tutte le informazioni sullo stato della sessione e le inserisce in ogni richiesta inviata al server attraverso il metodo POST inserendole nell'URL.

>[!done] Vantaggi
>- Facile da implementare
>- Non richiede l’introduzione di particolare funzionalità sul server

>[!danger] Svantaggi
>
>- Può generare lo scambio di grandi quantità di dati
>- Le risorse del server devono essere re-inizializzate ad ogni richiesta
