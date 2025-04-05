---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-03-28T14:19
updated: 2025-03-28T15:15
---


- **controllo di flusso:** non sovraccarica il destinatario
- **controllo di congestione:** se la rete è congestionata riduce i pacchetti inviati

## Struttura dei segmenti

Ogni segmento ha un intestazione (header) con delle informazioni aggiuntive:
- mittente
- destinatario
- numero di sequenza : numero che identifica il segmento (pacchetto) in particolare rappresenta il numero di 


## Connessione TCP

Percorso virtuale tra il mittente e il destinatario, sopra IP che è privo di connessione.

**3 fasi:**
1. Apertura della connessione
2. Trasferimento dei dati
3. Chiusura della connessione

>[!note] Apertura
>
>
>
>![[Pasted image 20250328143328.png|700]]

>[!note] push

## Dati Urgenti

I dati urgenti vengono elaborati subito indipendentemente della loro posizione (ad esempio anche se il pacchetto è arrivato in un ordine sbagliato).

Per fare ciò è attivata la flag `urgent` e i dati urgenti vengono inseriti all inzio del flusso, ed adtraverso il *Puntatore Urgente* si indica la fine dei dati urgenti e l’inizio dei dati normali.

>***Esempio:*** Utilizzato per indicare l'interruzione del data trasferimento dati.

## FSM (Finite State Machine)



## Normale Operativa


