---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-04-01T14:30
updated: 2025-04-07T18:25
---
## Controllo della congestione

Ci sono due principali approcci al controllo della congestione:

- **Controllo end-to-end** - La congestione è dedotta osservando le perdite e i ritardi nei sistemi terminali (utilizzato dal TCP).
- **Controllo assistito dalla rete** - I router forniscono un feedback ai sistemi terminali è utilizzato un singolo bit per indicare la congestione.

### Rilevamento Perdite

Lo stato di una rete può essere determinato in base alla quantità di perdita che è rilevata osservando gli eventi di **ACK duplicati** e/o **timeout**.

>[!note] Reazione in base allo stato della rete
>
>Se ACK arrivano in sequenza e con buona frequenza si può inviare e incrementare la quantità di segmenti inviati
>
>Se ACK duplicati o timeout è necessario ridurre la finestra dei pacchetti che si spediscono senza aver ricevuto riscontri
>
>***oss:*** TCP è auto-temporizzante: reagisce in base ai riscontri che ottiene.

### Slow Start

### Congestion Avoidance

## Versioni TCP

Esistono due principali versioni **TCP Taho** e **TCP Reno**.

>[!note] Taho

Miglioramenti fòdaksjfòlksajdf

>[!note] Reno
>
>Utilizza congestion avoidance, start recovery e slow start
>
>![[Pasted image 20250401145450.png|800]]

## Time Out

Il time out non può essere un valore assoluto, dovrà essere più grande del tempo di RTT che dipendere dalla congestione della rete e dalla distanza necessaria per raggiungere la destinazione.

Quindi dobbiamo effettuare una stima del RTT e determinare un valore di timeout superiore con un "margine di sicurezza".

>[!note] Rischi
>
>Stima del RTT:
>-  troppo piccola, provoca un timeout premature e quindi ritrasmissioni non necessarie
>- troppo grande, provoca una reazione lenta alla perdita dei segmenti

>[!note] Stima (SampleRTT)

# Esercizi

