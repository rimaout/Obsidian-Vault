---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-03-20T14:15
updated: 2025-03-20T15:07
---
# Introduzione Livello Trasporto

afdòkjklsòjf

## Indirizzamento

La maggior parte dei sistemi operativi è multiutente e multi-processo:
- Diversi processi client attivi (host locale)
- Diversi processi server attivi (host remoto)

Per stabilire una comunicazione tra i due processi è necessario un metodo per individuare:
- Host locale
- Host remoto
- Processo locale
- Processo remoto

>[!warning] Porta vs IP
>
>- Ad un *host* è associato un **indirizzo IP**.
>- Ad un *processo* è associata una **porta**

## Incapsulamento e Decapsulamento



## Multiplexing e Demultiplexing

- [[#^a89c62|Demultiplexing]]
- [[#^3886db|Multiplexing]]

>[!note] Demultiplexing

^a89c62

>[!note] Multiplexing

^3886db

## Socket

Le socket sono delle astrazioni create ed utilizzate dai programmi applicativi utilizzate per la comunicazione tra un processo client e un processo server significa comunicare tra due socket create nei due lati di comunicazione.

Una socket é una struttura dati che nella sua forma più semplice è composta da due informazioni un indirizzo IP e un numero di porta.

![[Pasted image 20250320142951.png|800]]

>[!note] Numero di Porta


#### Individuare un Socket

>[!note] Lato Client

>[!note] Lato server
>
>Su due processi client diversi comunicano allo stesso processo server vedranno un socket address diverso, con l'indirizzo ip uguale ma numero porta diverso.
>
>kjlkajdfskl

## Servizi dei protocolli di trasporto Internet 

- [[Protocollo UDP (User Datagram Protocol)]]

# Protocollo UDP (User Datagram Protocol)

kjsslkdzjf

Servizio senza connessione
- è il mittente che deve preoccuparsi di dividere i pacchetti in dimensioni ottimali per l'invio 
- ogni pacchetto è indipendente dagli altri (ordine d'arrivo potrebbe essere diverso rispetto all'ordine d'arrivo)


![[Screenshot 2025-03-20 at 14.47.40.png|800]]

## Rappresentazione FSM

Il comportamento di un protocollo di trasporto può essere rappresentato da un automa a stati finiti (FSM - Finite State Machine).

## Struttura dei datagrammi

![[Pasted image 20250320145301.png|500]]

## Checksum

![[Pasted image 20250320145812.png|800]]

Volgiamo calcolare il checksum di una sequenza di 32 bit la divido a metà ottenendo due sequenze da 16 faccio la somma, il risulato è le checksum. Ora se mando la stringa posso inviare anche la checksum, cosi il ricevente può ricalcolarla per vedere se coincide.

## Verso TCP

1. Comunicazione tra processi con Indirizzamento mediante numero di porta
2. Incapsulamento/decapsulamento (frammenti)
3. Multiplexing/demultiplexing
4. Trasporto orientato alla connessione
5. Controllo di flusso
6. Controllo degli errori
7. Controllo della congestione

prime tre sono anche dell'udp

### Servizio orientato alla conessione

