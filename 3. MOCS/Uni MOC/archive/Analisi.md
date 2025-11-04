---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2025-10-28T19:27
updated: 2025-10-30T14:29
---
## Oggetti

*Utente:*
- ID auto-generato (univoco, non modificabile) (id)
- Username (modificabile, univoco)
- Foto profilo

*Conversazione:*
- ID auto-generato (univoco, non modificabile) (id)
- Messaggi
- Può essere singola o gruppo (complete disjoint)

*Conversazione Singola:* 
- 2 utenti (univoco)

*Conversazione Gruppo:*
- Membri (>= 1)
	- utente può essere utente_partecipe o utente_uscito
- Foto
- Nome

*Messaggio:*
- ID auto generato (id)
- conversazione
- utente mittente
- orario invio
- testo
- foto
- testo + foto
- utenti riceventi: lista di coppie (id utente, timestamp)
- utenti lettori: lista di coppie (id utente, timestamp)
- flag cancellato (se cancellato il testo e l’immagine devo essere svuotati)
- flag inoltrato

*Messaggio Risposta:* estende messaggio
- messaggio a cui si risponde (deve essere contenuto nella stessa chat)
- il messaggio non deve essere cancellato ?

*Reazione:*
- messaggio a cui si reagisce (id)
- codice emoji 
- utente che reagisce (id)

**Operazioni:**

*Lista Conversazioni (getConversazioni):*
- un utente può richiedere le sue conversazioni
- presentate in ordine cronologico (in base al ultimo messaggio inviato in ogni conversazione)
- Informazioni delle conversazioni: nome (gruppo/utente), foto profilo, data ora ultimo messaggio + anteprima messaggio (foto o testo)

*Ricerca utente:* Possibilità di cercare utenti tramite user name.

*Creare Nuova Conversazione (singola):* chat con un qualsiasi utente di wasapp

*Creare nuovo gruppo:* 

*Abbandono Gruppo:*

*Aggiungi persona a gruppo:* solo se partecipi al gruppo (e sei non uscito) puoi aggiungere un altra persona

*Visualizza Chat:*  Ritorna i messaggi ordinato in ordine cronologico inverso

*Invio Messaggio:* in una conversazione

*Cancella Messaggio:* metti flag e cancella testo/immagine, si può fare solo a messaggi inviati da te (l'immagine va cancellata veramente??)

*Modifica nome:* l'utente può modificare il proprio username, purché il nuovo nome non sia già utilizzato



