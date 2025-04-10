---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-04-09T17:42
updated: 2025-04-09T18:10
---
## Introduzione

Il protocollo TCP è un servizio **affidabile** ed **orientato alla connessione**, per questo è richiesto un setup fra i processi *client* e *server*.

>[!note] Servizi Forniti
>Stesse cose fornite dal [[Protocollo UDP (User Datagram Protocol)|UDP]]:
>- Comunicazione tra processi utilizzando i [[Introduzione Livello Trasporto#Socket|Socket]]
>- [[Introduzione Livello Trasporto#Incapsulamento e Decapsulamento|Multiplexing/demultiplexing]] dei pacchetti
>- [[Introduzione Livello Trasporto#Incapsulamento e Decapsulamento|Incapsulamento e decapsulamento]]
>  
>Inoltre fornisce funzionalità avanzate come:
>- **Trasporto affidabile** fra i processi di invianti e riceventi.
>- **Controllo di flusso:** il mittente cerca di non sovraccaricare il destinatario
>- **Controllo della congestione:** Riduce i dati inviati quando le rete è sovraccaricata

>[!note] Servizi non Forniti
>
>Non fornisce temporizzazione, garanzie su un ampiezza di banda minima, sicurezza (alcune possono essere implementate, es. SSL)

>[!warning] Flusso di Byte
>
 >Una delle differenze con il protocollo UDP è che la comunicazione tra mittente e ricevente può essere vista come un flusso di byte e non come un invio di pacchetti.
 >
 >![[Pasted image 20250409180026.png|1000]]

## Demultiplexing orientato alla connessione

La socket TCP è identificata da 4 parametri:
- *Indirizzo IP* e *porta di origine*
- *Indirizzo IP* e *porta di destinazione*

Un host server può supportare più socket TCP contemporanee dato che ogni socket è identificata dai 4 parametri. Si avrà una socket differente anche per lo stesso client, ogni richiesta viene trasmessa su una diversa socket.

Essenzialmente il server accetta tutte le connessioni sulla stessa socket e poi le sposta su una porta differente.

![[Pasted image 20250409180957.png|800]]