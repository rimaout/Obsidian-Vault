---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-03-13T14:21
updated: 2025-03-13T15:37
---
## Evoluzione Apps Internet

![[Pasted image 20250313142228.png|700]]

## World Wide Web

**World Wide Web (WWW)** è un applicazione Internet nata dalla necessità di scambio e condivisione di informazioni tra ricercatori universitari di varie nazioni.

>[!note] Caratteristiche
>
>- Opera su richiesta (on demand)
>- Facile rendere informazioni disponibili 
>- Collegamenti ipertestuali (hyperlinks) e motori di ricerca permettono di navigare su una grande quantità di siti


>[!note] Componenti
>
>dkjfalòskfjlksj
>
>![[Pasted image 20250313142728.png|600]]

## Terminologia

Una pagina web è costituita da oggetti

Un oggetto può essere un file HTML, un’immagine JPEG, un’applet Java, un file audio, ...

Una pagina web è formata da un file base HTML (HyperText Markup Language) che include diversi oggetti referenziati

Ogni oggetto è referenziato da un URL (Uniform Resource Locator), ovvero un file che può essere ottenuto attraverso un URL

## URL

fsadlkjhdskaj

Quando non scriviamo nessuna porta viene utilizzata la porta standard 80

## Tipo di Documenti 


## HTTP


### Connessione HTTP

Attualmente si utilizzano connessioni persistenti


sdkfjalkòsdfjlòka

Le connessioni persistenti i client manda richieste sequenziali, nelle connessioni non persistenti invece si possono richiedere più connessioni parallele, che teoricamente può rendere il trasferimento dei file più veloce ma richiederebbe troppo overhead per la gestione.

## Richiesta 

Formato richiesta
![[Pasted image 20250313145606.png|600]]

Intestazione richiesta (usa mb table)
![[Pasted image 20250313145315.png|600]]




>[!note] Codici di stato
>
## Risposta

![[Pasted image 20250313145358.png|600]]

![[Pasted image 20250313145502.png|600]]

# Cookie

HTTP è un protocollo "senza stato" ovvero il server una volta servito il client se ne dimentica non mantiene informazioni sulle richieste fatte. Questo perché I protocolli che mantengono lo “stato” sono complessi.

Ci sono molti casi in cui il server ha bisogno di ricordarsi degli utenti, per questo si possono usare i Cookie.

Il meccanismo dei Cookie rappresenta un modo per creare una sessione di richieste e risposte HTTP “con stato” (stateful).

## Sesione

La sessione rappresenta un contesto più largo rispetto alla richiesta/risposta.

Ci possono essere diversi tipi di sessione in base al tipo di informazioni scambiate e la natura del sito.

>[!note] Caratteristiche
>
>Caratteristiche generali di una sessione:
>
>1. Ogni sessione ha un inizio e una fine.
>2.  Ogni sessione ha un tempo di vita relativamente corto. 
>3. Sia il client che il server possono chiudere la sessione. 
>4. La sessione è **implicita** nello scambio di informazioni di stato

>[!example] Esempio
>
>![[Screenshot 2025-03-13 at 15.25.36.png|500]]
>
>Dopo la prima richiesta del client, il server invia un set-cookie per inizializzare il cookie nel client.
>
>Il client utilizzera quelo coockie in ogni risposta/richiesta al server per identificarsi.
>

## Caching


