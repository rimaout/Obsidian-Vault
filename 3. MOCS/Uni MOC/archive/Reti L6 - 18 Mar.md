---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-03-18T14:21
updated: 2025-03-21T15:13
---
## File Transfer Protocol (FTP)

## Connessione Dati

## Comandi e Risposte

>[!note] Comandi
>
>Esiste una corrispondenza uno a uno tra il comando immesso dall’utente e quello FTP inviato sulla connessione di controllo.
>
>| Comando | Argomento |  Descrizione |
>| --- | --- | --- |
>| USER | username |  |
>| PASS | password | |
>| LIST | | |
>| RETR | | |
>| STOR | | |
>
>>***oss:*** Inviati come testo ASCII sulla connessione di controllo

>[!note] Codici di Risposta
>
>Ciascun comando ricevuto da un server è seguito da sua risposta spedita al client (codice di ritorno).
>
>

## PostaElettronica

**Struttura Generale:**

![[Pasted image 20250318143404.png|700]]


### User Agent



## Protocolli 

![[Pasted image 20250318143844.png|800]]


### Protocollo SMTP

Tre fasi:
- Handshaking
- trasferimento di messaggi
- chiusura

>[!example] Esempio
>
>![[Pasted image 20250318143751.png|700]]


### Protocollo MIME

Converte file multimediali in ASCI in modo tale da essere inviati via email

![[Screenshot 2025-03-18 at 14.46.40.png|800]]

In questo caso si fa encoding di un imagine jpeg in dati in base 64

### Protocollo POP3

permette al client di destinazione di ricevere la posta, 

 Quando la connessione è stabilita si procede in 3 fasi
1. **Autorizzazione**: L’agente utente invia nome utente e password per essere identificato
2. **Transazione**: L’agente utente recupera i messaggi
3. **Aggiornamento**: Dopo che il client ha inviato il QUIT, e quindi conclusa la connessione, vengono cancellati i messaggi marcati per la rimozione.
   
### Protocollo IMAP


>[!question] Differenza tra POP3 e IMAP
>

