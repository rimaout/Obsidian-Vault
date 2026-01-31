---
type: Uni Note
class: "[[Basi di Dati 2 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-04-09T17:22
updated: 2026-01-31T13:32
---
## Introduzione

L'UDP è un protocollo di trasporto **inaffidabile** e **senza connessione**.

>[!note] Servizi Forniti
>
>- Comunicazione tra processi utilizzando i [[Introduzione Livello Trasporto#Socket|Socket]]
>- [[Introduzione Livello Trasporto#Incapsulamento e Decapsulamento|Multiplexing/demultiplexing]] dei pacchetti
>- [[Introduzione Livello Trasporto#Incapsulamento e Decapsulamento|Incapsulamento e decapsulamento]]

>[!note] Servizi non Forniti
>
>Non fornisce alcun setup della connessione, affidabilità, controllo di flusso, controllo della congestione, controllo errori (eccetto ckecksum) temporizzazione né ampiezza di banda minima e sicurezza.

## Servizio Connectionless

L'UDP è un servizio senza connessione, questo vuol dire che la comunicazione è unilaterale e che non è possibile ricevere riscontri sul risultato della invio di un messaggio.

Per questo motivo **non** è possibile effettuare il **control flow**, **controllo di congestione** o **controllo errori** , ed il mittente invia datti a raffica senza pensare al destinatario:
- È il mittente che deve preoccuparsi di dividere i pacchetti in dimensioni ottimali per l'invio.
- Ogni pacchetto è indipendente dagli altri (ordine d'arrivo potrebbe essere diverso rispetto all'ordine d'arrivo)

![[Screenshot 2025-03-20 at 14.47.40.png|800]]

## Datagrammi UDP

Il processo mittente non può inviare un flusso di dati e aspettarsi che UDP lo suddivida in datagrammi correlati per questo è compito dei processi inviare richieste di dimensioni sufficientemente piccole per essere inserite ciascuna in un singolo datagramma utente.

Solo i processi che usano messaggi di dimensioni inferiori a 65507 byte (65535 – 8 byte di intestazione UDP e 20 byte di intestazione IP) possono utilizzare il protocollo UDP

>[!note] Struttura Datagramma UDP
>
>![[Pasted image 20250320145301.png|500]]

## Checksum

Il checksum è una tecnica che permette al ricevente di determinare se durante il trasporto sono avvenute delle alterazioni (errori) sul datagramma trasmesso.

>[!note] Mittente
>
>1. Il messaggio viene diviso in parole da 16 bit
>2. Il valore checksum viene inizialmente impostato a 0
>3. Tutte le parole del messaggio incluso il checksum vengono sommate usando l'addizione complemento ad uno
>4. Viene fatto il complemento ad uno della somma e il risultato è il checksum
>5. Il checksum viene inviato assieme ai dati

>[!note] Ricevente
>
>1. Riceve il messaggio (che comprende il checksum)
>2. Il messaggio viene diviso in parole da 16 bit
>3. Tutte le parole vengono sommate usando l'addizione a complemento ad uno
>4. Viene fatto il complemento ad uno della somma e il risultato diventa il nuovo checksum
>5. Se il valore del checksum è 0 allora il messaggio viene accettato altrimenti viene scartato

![[Pasted image 20250320145812.png|700]]

Vedi anche [Esempio Neso Academy](https://www.youtube.com/watch?v=AtVWnyDDaDI).
## Utilizzi

Questo protocollo è utilizzato per l'invio di dati non richiedono affidabilità come ad esempio streaming video o telefonia internet come Skype.

>[!note] DNS utilizza UDP
>
>Quando vuole effettuare una query, DNS costruisce un messaggio di query e lo passa a UDP:
>1. L’entità UDP aggiunge i campi di intestazione al messaggio e trasferisce il segmento risultante al livello di rete, etc.
>2. L’applicazione DNS aspetta quindi una risposta
>3. Se non ne riceve tenta di inviarla a un altro server dei nomi
>
>La semplicità della richiesta/risposta (molto breve) motiva l’utilizzo di UDP, che risulta più veloce:
>- Nessuna connessione stabilita
>- Nessuno stato di connessione
>- Intestazioni di pacchetto più corte