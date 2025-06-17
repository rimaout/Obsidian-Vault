---
type: Uni Note
class: "[[Reti (class)]]"
academic year: 2024/2025
related: 
completed: true
created: 2025-04-07T18:00
updated: 2025-04-12T20:20
---
## File Transfer Protocol (FTP)

L'FTP è un programma per il trasferimento di file da un host ad un altro host remoto; si basa sul modello client/server:
- ***client***: il lato che inizia il trasferimento
- ***server***: host remoto

Quando l’utente fornisce il nome dell’host remoto, il processo client FTP stabilisce una connessione TCP sulla porta 21 con il processo server FTP.

In realtà vengono stabilite due connessioni:
1. [[#^f59594|Connessione di Controllo]]
2. [[#^f18913|Connessione Dati]]

![[Pasted image 20250324114153.png|800]]

>[!note] Connessione di Controllo
>
>Connessione instaurata sulla porta 21, si occupa del trasferimento delle informazioni di controllo. È utilizzata per scambiare i comandi come ad esempio il cambio di directory o l'invio di username e password.
>

^f59594

>[!note] Connessione Dati
>
>Quando il server riceve un comando per trasferire un file (es. get, put), apre una connessione dati TCP sulla porta 20 con il client.
>
>Dopo il trasferimento di un file, il server chiude la connessione, quindi si crea una nuova connessione per ogni file trasferito.

^f18913

### Comandi e Risposte

>[!note] Comandi
>
>Esiste una corrispondenza uno a uno tra il comando immesso dall’utente e quello FTP inviato sulla connessione di controllo.
>
>|Comando|Argomenti|Descrizione|
>|---|---|---|
>|ABOR||Interruzione del comando precedente|
>|CDUP||Sale di un livello nell'albero delle directory|
>|CWD|Nome della directory|Cambia la directory corrente|
>|DELE|Nome del file|Cancella il file|
>|IST|Nome della directory|Elenca il contenuto della directory|
>|MKD|Nome della directory|Crea una nuova directory|
>|PASS|Password utente|Password|
>|PASV||Il server sceglie la porta|
>|PORT|Numero di porta|Il client sceglie la porta|
>|PWD||Mostra il nome della directory corrente|
>|QUIT||Uscita dal sistema|
>|RETR|Nome di uno o più file|Trasferisce uno o più file dal server al client|
>|RMD|Nome della directory|Cancella la directory|
>|RNTO|Nome (del nuovo) file|Cambia il nome del file|
>|STOR|Nome di uno o più file|Trasferisce uno o più file dal client al server|
>|USER|Identificativo|Identificazione dell'utente|
>
>>***oss:*** Inviati come testo ASCII sulla connessione di controllo

>[!note] Codici di Risposta
>
>Ciascun comando ricevuto da un server è seguito da sua risposta spedita al client (codice di ritorno).
>
>|Codice|Descrizione|Codice|Descrizione|
>|---|---|---|---|
>|125|Connessione dati aperta|250|Azione sul file OK|
>|150|Stato del file OK|331|Nome dell'utente OK; in attesa della password|
>|200|Comando OK|425|Non è possibile aprire la connessione dati|
>|220|Servizio pronto|450|Azione sul file non eseguita; file non disponibile|
>|221|Servizio in chiusura|452|Azione interrotta; spazio insufficiente|
>|225|Connessione dati aperta|500|Errore di sintassi; comando non riconosciuto|
>|226|Connessione dati in chiusura|501|Errore di sintassi nei parametri o negli argomenti|
>|230|Login dell'utente OK|530|Login dell'utente fallito|

>[!example] Esempio
>
>![[Pasted image 20250325131939.png|600]]

## Posta Elettronica (SMTP, POP3, IMAP)

### Struttura generale 

I sistema della posta elettronica si basa su tre componenti principali:
- [[#^19f62c|User agent]]: usato per scrivere e inviare un messaggio o leggerlo
- [[#^bcb02c|Message Transfer Agent]]: usato per trasferire il messaggio attraverso Internet
- *Message Access Agent*: usato per leggere la mail in arrivo

![[Pasted image 20250318143404.png|700]]

>[!note] User Agent (UA)
>
>Lo user agent (o mail reader) è attivato dall’utente o da un timer e fornisce funzionalità di:
>- composizione
>- editing
>- lettura dei messaggi di posta elettronica
>  
>I messaggi (mail) in uscita o in arrivo sono memorizzati sul server associato al User Agent. I messaggi in uscita dal agent vengo trasferiti attraverso il [[#^bcb02c|message transfer agent]].

^19f62c

>[!note] Message Transfer Agent (MTA)
>
>Il Mail Transfer Agent si occupa di trasferire le mail da un User Agent al suo server di posta elettronica, o del trasferimento delle mail tra due server di posta elettronica.
>
>In generale permette di tramettere messaggi via internet, utilizzando il protocollo [[#SMTP (Simple Mail Transfer Protocol)]]
>
>Come comunicano gli MTA? - i server di posta hanno:
>- *Casella di posta* (mailbox) contiene i messaggi in arrivo per l’utente
>- *Coda di messaggi* da trasmettere (tentativi ogni x minuti per alcuni giorni)

^bcb02c

### Protocolli

Per il trasferimento delle mail si utilizzando diversi tipi di protocolli.

Per l'invio di mail da *client* ad un *server* si utilizzando:
- [[#SMTP (Simple Mail Transfer Protocol)]]
- [[#MIME (Multipurpose Internet Mail Extension)]]
  
Per l'invio di mail da un *server* ad un *client* si utilizzano:
- [[#Protocollo POP3 (Post Office Protocol)]]]
- [[#Protocollo IMAP (Internet Message Access Protocol)]]

![[Pasted image 20250318143844.png|800]]

### SMTP (Simple Mail Transfer Protocol)

Questo protocollo utilizza una connessione TCP  per trasferire in modo affidabile i messaggi di posta elettronica (porta utilizzata 25).

La comunicazione tra client e server è composta da 3 fasi:
- Handshaking
- Trasferimento di messaggi
- Chiusura

>[!note] Formato Messaggi SMTP
>
>Per il formato si utilizza lo standard RFC 822, composto da un intestazione ed un corpo.
>
>L'**intestazione** ha le seguenti sezioni:
>
>![[Pasted image 20250407170451.png|650]]
>
>Il **corpo** non è altro che una sequenza di *caratteri ASCII*.

>[!warning] Testo ASCII
>
>Questo protocollo permette di inviare soltanto caratteri con formattazione ASCII 7 bit, sia per i comandi che per i messaggi (mail) inviati.

>[!note] Funzionamento Scambio Mesaggi
>
>Il client SMTP (che gira sull’host server di posta in invio) fa stabilire una connessione sulla porta 25 verso il server SMTP (che gira sull’host server di posta in ricezione).
>1. Se il server è inattivo il client riprova più tardi
>2. Se il server è attivo, viene stabilita la connessione
>3. Il server e il client effettuano una forma di handshaking (il client indica indirizzo email del mittente e del destinatario)
>4. Il client invia il messaggio
>5. Il messaggio arriva al server destinatario grazie all’affidabilità di TCP
>6. Se ci sono altri messaggi si usa la stessa connessione (**connessione persistente**), altrimenti il client invia richiesta di chiusura connessione

>[!example] Esempio
>
>![[Pasted image 20250318143751.png|700]]

### MIME (Multipurpose Internet Mail Extension)

Il protocollo MIME consente di inviare file multimediali via mail, convertendoli e de-convertendoli in caratteri ASCII 7bit.

![[Pasted image 20250407170657.png|700]]

>[!note] Formato Invio
>
>Per inviare contenuti diversi dal testo ASCII si usano intestazioni aggiuntive
>
>![[Screenshot 2025-03-18 at 14.46.40.png|700]]

>[!note] Formato Ricezione
>
>Un’altra classe di righe di intestazione viene inserita dal server di ricezione SMTP
>
>In particolare il server di ricezione aggiunge **Received** in cima al messaggio, che specifica il nome del server che ha inviato il messaggio (from), il nome del server che lo ha ricevuto (by), e l’orario di ricezione.
>
>![[Pasted image 20250407171228.png|700]]

### Protocollo POP3 (Post Office Protocol)

Permette al client di destinazione di ricevere la posta.

 Quando la connessione è stabilita si procede in 3 fasi
1. **Autorizzazione**: L’agente utente invia *nome utente* e *password* per essere identificato
2. **Transazione**: L’agente utente recupera i messaggi
3. **Aggiornamento**: Dopo che il client ha inviato il `QUIT`, e quindi conclusa la connessione, vengono cancellati i messaggi marcati per la rimozione.

>[!note] Comandi
>
>Comandi utilizzabili con POP3, possiamo distinguerli in due fasi della comunicazione:
>
>Fase di Autorizzazione
>- `user` dichiara il nome dell’utente
>- `pass` password
>- Il server può rispondere con `+OK` o `-ERR`
>
>Fase di Transazione
>- `list` elenca i numeri dei messaggi
>- `retr` ottiene i messaggi in base al numero
>- `dele` cancella
>- `quit`
>
>![[Pasted image 20250407175243.png|600]]

>[!note] Protocollo locale senza stato
>
>Con il POP3 quindi, usando la modalità “scarica e cancella” non possiamo rileggere le mail se cambiamo client, queste infatti non saranno più disponibili sul server.
>
>L’utente infatti non può nemmeno creare cartelle o altro sul server, va tutto creato in locale sul proprio computer.

### Protocollo IMAP (Internet Message Access Protocol)

IMAP consente di **creare cartelle anche sul server** e di organizzare quindi i messaggi **mantenendo lo stato** delle sessioni dell’utente.

Il protocollo per fare questo associa a una cartella ogni messaggio arrivato dal server e poi fornisce agli utenti dei comandi per:
- Creare cartelle e spostare messaggi da una cartella all’altra
- Effettuare ricerche nelle cartelle del server Mantengono informazioni su:
- Nomi cartelle
- Associazioni messaggi - cartelle

Inoltre vengono forniti comandi per ottenere le componenti dei messaggi:
- Intestazione
- Corpo del messaggio

## HTTP

Alcuni mail server consentono l’accesso tramite web ovvero tramite HTTP, in questo caso l’agente utente diventa il browser e comunica con il suo mailbox tramite HTTP e anche il ricevente usa HTTP per accedere alla mailbox.