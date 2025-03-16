---
type: Uni Note
class: "[[Reti (class)]]"
academic year: 2024/2025
related: 
completed: false
created: 2025-03-13T11:59
updated: 2025-03-13T12:02
---
## Introduzione

Fino ad ora abbiamo visto come è [[Struttura delle Reti|strutturata una rete]] e come si [[Capacità e Prestazioni di una Rete|misurano le prestazioni]], tuttavia per poter comunicare non è sufficiente la presenta dei collegamenti (hardware) ma è necessario anche il software sotto forma di [[#^624269|protocolli]] di comunicazione.

>[!note] Protocollo
>
>Un protocollo definisce le regole che il mittente e il destinatario, così come tutti i sistemi intermedi coinvolti, devono rispettare per essere in grado di comunicare.
>
>In situazioni più complesse viene effettuato **layering di protocolli**, ovvero i compiti vengono suddivisi fra più livelli ognuno con un suo protocollo.

^624269

>[!note] Struttura a Livelli 
>
>La strutturazione dei protocolli in livelli consente di suddividere un compito complesso in compiti più semplici.
>
>
>
>![[Screenshot 2025-03-11 at 14.25.12.png|600]]

## TCP/IP

TCP/IP è una famiglia di protocolli attualmente utilizzata in Internet ed organizzata in uno stack (gerarchia) di livelli detti moduli.

>[!note] Layering
>
>Lo scopo di ogni strato è quello di **offrire** determinati [[#^d46d4c|servizi]] agli strati di livello superiore, nascondendo i dettagli di implementazione.
>
>Le entità che formano gli strati sono chiamati **pari** (peer) e comunicano usando il protocollo.
>
>**Vedi approfondimento:** [[#Layering]]

>[!note] Servizzi
>
>Un servizio è un insieme di primitive che uno strato offre a quello superiore.
>
>Definisce quali operazioni lo strato è in grado di offrire, ma non dice nulla di come queste operazioni sono implementate.

^d46d4c

### Stack protocollare 

La pila TCP/IP è composta di cinque livelli:

![[Pasted image 20250311143058.png|600]]

>[!note] Livello Applicazione
>
>Protocollo che regola l'interazione tra applicazioni di rete, in questo livello i *pacchetti* sono chiamati *messaggi*.
>
>>***Esempio protocolli:*** HTTP, SMTP, FTP, DNS

>[!note] Trasporto
>
>Si occupa del **trasferimento dei messaggi** da un applicazione ad un altra, in questo livello i *pacchetti* sono chiamati *segmenti*.
>
>Esistono due protocolli:
>- `TCP` affidabile, ma più lenta.
>- `UDP` non affidabile, ma più veloce.

>[!note] Rete
>
>Livello che implementa l'**instradamento (routing) dei segmenti** dall'origine alla destinazione, in questo livello i *pacchetti* sono chiamati *datagrammi*.
>
>>***Esempio protocolli:*** IP

>[!note] Link
>
>Livello che trasmette datagrammi da un nodo a quello successivo sul percorso, in questo livello i *pacchetti* sono chiamati *frame*.
>
>>***Esempio protocolli:*** Ethernet, Wi-Fi, PPP (Lungo un percorso sorgente-destinazione un diatagramma può essere gestito da protocolli diversi)
>

>[!note] Fisico
>
>Riguarda il trasferimento fisico dei singoli bit in un mezzo di trasmissione.

### Dove si trova il software di rete?

Non tutti i sistemi contengono tutti i moduli infatti grazie al layering i sistemi implementano solo i livelli necessari per i loro compiti, riducendo la complessità:

- I **terminali** contengono tutto lo stack protocollare
- I **switch** contengono soltanto i moduli *link* e *fisico*
- I **router** rispetto agli switch contengono anche il modulo `rete`, perché si occupano del routing dei pacchetti.

![[Screenshot 2025-03-11 at 14.45.01.png|700]]

### Incapsulamento e decapsulamento

La sorgente effettua l’incapsulamento (prende il pacchetto dal livello superiore, lo considera come carico dati o payload e aggiunge un header o intestazione).

- *Messaggio* = nessuna intestazione
- *Segmento* = header trasporto + messaggio
- *Datagramma* = header rete + segmento
- *Frame* = header collegamento + datagramma

![[Screenshot 2025-03-13 at 11.42.13.png|700]]

>[!warning] Osservazioni
>- Il destinatario effettua il decapsulamento.
>- Il router effettua sia incapsulamento che decapsulamento perché collegato a due link.

### Multiplexing e Demultiplexing

Dato che lo stack protocollare TCP/IP prevede più protocolli nello stesso livello, è necessario eseguire il multiplexing alla sorgente e il demultiplexing alla destinazione.

**Multiplexing** - un protocollo può incapsulare (uno alla volta) i pacchetti ottenuti da più protocolli del livello superiore.

**Demultiplexing** - un protocollo può decapsulare e consegnare i pacchetti a più protocolli del livello superiore.

![[Pasted image 20250311145644.png|700]]

### Indirizzi 

Il modello TCP/IP prevede una comunicazione logica tra coppie di livelli, per questo è necessario avere un indirizzo sorgente e un indirizzo destinazione ad ogni livello.

![[Pasted image 20250313115447.png|600]]

## Layering

>[!done] Vantaggi
>
>L'utilizzo di questa struttura a livelli ha permesso di rendere il sistema **modulare**, questo offre vantaggi come:
>- Semplicità di design
>- Possibilità di modificare un modulo in modo trasparente se le interfacce con gli altri livelli rimangono le stesse
>- Possibilità per ciascun costruttore di adottare la propria implementazione di un livello purché i requisiti su interfacce rimangono soddisfatti.

>[!danger] Svantaggi
>
>A volte necessario scambio di informazioni tra livelli non adiacenti (esempio: per ottimizzare app funzionante su wireless) non rispettando principio della stratificazione.