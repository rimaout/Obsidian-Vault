---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-04-08T14:19
updated: 2025-04-08T15:09
---
## Funzioni Chiave (routing and forwarding)

- **Instradamento** (routing): determina il percorso seguito dai pacchetti dall’origine alla destinazione
- **Inoltro** (forwarding): trasferisce i pacchetti dall’input di un router all’output del router appropriato

Queste operazioni sono rese possibili attraverso:
- **Routing algorithm**: crea la forwarding table (determina i valori inseriti nella tabella)
- **Forwarding table**: specifica quale collegamento di uscita bisogna prendere per raggiungere la destinazione

![[Screenshot 2025-04-08 at 14.25.07.png|600]]

## Switch e Router



## Circuit switching vs. Packet switching



## ATM (Asynchronous transfer mode)

É una rete progettata nei primi anni 90 ed è orientata alla concessione. Il suo scopo era quello di unificare unificare voce, dati, televisione via cavo, etc; ma attualmente è utilizzata nella rete telefonica per trasportare (internamente) pacchetti IP.

Le connessioni vengono chiamate circuiti virtuali (in analogia con quelli telefonici che sono circuiti fisici). Quando una connessione è stabilita, ciascuna parte può inviare dati (suddivisi in celle di 53 bytes).

## Reti a Datagramma

òdfjslkòadfj

## Livello di Rete

### Router

I router implementano 3 livelli dello [[Introduzione allo stack protocollare TCP-IP|stack protocollare TCP-IP]]:
- **Fisico**
- **Collegamento**
- **Rete**

![[Pasted image 20250408144159.png|800]]

## Porte Uscita

**Funzionalità di accodamento:*** quando la struttura di commutazione consegna pacchetti alla porta d’uscita a una frequenza che supera quella del collegamento uscente.

**Schedulatore di pacchetti:** stabilisce in quale ordine trasmettere i pacchetti accodati.


## Protocolli a livello di Rete

A livello di rete ci sono diversi protocolli di cui alcuni dei più importanti ed utilizzati sono:
- IP: Internet Protocol v4 (anche v6)
- IGMP: Internet Group Management Protocol (multicasting)
- ICMP: Internet Control Message Protocol (gestione errori)
- ARP: Address Resolution Protocol (associazione indirizzo IP – ind. collegamento)
+ Protocolli di Routing

### IPv4

Il protocollo IPv4 è responsabile della suddivisione in pacchetti, dell’inoltro (forwarding), e della consegna dei datagrammi al livello di rete (host to host), queste sono le sue caratteristiche:

- **Inaffidabile**, senza connessione, basato su datagrammi
- Offre un servizio di consegna **best effort**

>[!note] Formato Datagramma
>
>- ***Numero di versione***: consente al router la corretta interpretazione del datagrammaIPv4 o IPv6.
>- ***Lunghezza dell’intestazione***: un datagramma IP può contenere un numero variabile di opzioni (incluse nell’intestazione), questi bit indicano dove inizia il campo dati.
>- ***Tipo di servizio***: serve per distinguere diversi datagrammi con requisiti di qualità del servizio diverse (realtime)
>- ***Lunghezza del datagramma***: lunghezza totale (in byte) del datagramma IP inclusa l’intestazione. Serve per capire se il pacchetto è arrivato completamente.
>- ***Identificatore***, ***flag*** e ***offset di frammentazione***: questi tre campi servono per gestire la frammentazione dei pacchetti (IPv6 non prevede frammentazione).
>- ***Tempo di vita***: o time to live (TTL) assicura che i datagrammi non restino in circolazione per sempre nella rete. Il campo viene ddecrementato a ogni hop e il datagramma viene eliminato in caso il suo `TTL = 0`.
>- ***Protocollo***: indica il protocollo a livello di trasporto al quale va passato il datagramma. Questo campo è utilizzato solo quando il datagramma raggiunge la destinazione finale. (es. TCP, UDP, ICMP, IGMP, OSPF)
>- ***Checksum dell’intestazione***:
>- ***Indirizzi IP di origine e destinazione***:
>- ***Opzioni***:
>- ***Dati***:  
