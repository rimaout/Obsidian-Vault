---
type: Uni Note
class: "[[Reti (class)]]"
academic year: 2024/2025
related: 
completed: true
created: 2025-05-10T14:02
updated: 2025-06-15T17:04
---
## ICMP

L'Internet Control Message Protocol fa parte del livello di rete e ha il compito di **notificare** agli host lo stato e gli errori dei router.

Queste notifiche sono inserite all'interno del campo dati dei datagrammi IP.

Infatti nell’[[Internet Protocol v4 (IPv4) - Indirizzamento, DHCP, NAT, Forwarding|IPv4]] ci sono diversi problemi non gestiti:
- Se un router deve scartare un pacchetto perché non sa dove instradarlo cosa si fa?
- Se un datagramma ha il campo TTL pari a 0?
- Se un host non riceve tutti i frammenti di datagramma entro un limite di tempo?

Grazie a ICMP il router che riscontra l’errore può inviare i dettagli di questo all’host mittente sperando che le informazioni che invia siano sufficienti a risolvere il problema per l’invio successivo.

I messaggi che invia hanno un campo tipo e un campo codice, contengono l’intestazione e i primi 8 byte del datagramma IP che ha causato l’errore.

| Tipo | Codice | Descrizione                          |
| ---- | ------ | ------------------------------------ |
| `0`  | `0`    | risposta eco (a ping)                |
| `3`  | `0`    | rete destin. irraggiungibile         |
| `3`  | `1`    | host destin. irraggiungibile         |
| `3`  | `2`    | protocollo dest. irraggiungibile     |
| `3`  | `3`    | porta destin. irraggiungibile        |
| `3`  | `6`    | rete destin. sconosciuta             |
| `3`  | `7`    | host destin. sconosciuto             |
| `4`  | `0`    | riduzione (controllo di congestione) |
| `8`  | `0`    | richiesta eco                        |
| `9`  | `0`    | annuncio del router                  |
| `10` | `0`    | scoperta del router                  |
| `11` | `0`    | TTL scaduto                          |
| `12` | `0`    | errata intestazione IP               |

## Ping

 Il programma `ping` funziona inviando datagrammi contenenti un `echo request` di ICMP, a un indirizzo IP specifico. 
 
Se il dispositivo di destinazione riceve il pacchetto, risponde con un altro pacchetto, chiamato `echo reply`. 

Il programma `ping` *misura il tempo* che intercorre *tra l'invio* del pacchetto e la *ricezione* della risposta.

## Tracerout

Il programma `traceroute` è uno strumento utilizzato per visualizzare il percorso che i pacchetti di dati seguono per raggiungere un determinato indirizzo IP.

Invia una serie di datagrammi IP alla destinazione, ciascuno contenente un segmento UDP aventi inizialmente TTL (time to live) basso che aumenta gradualmente ad ogni passaggio. Il primo `TTL = 1`, il secondo `TTL = 2`, ecc.

Quando l’n-esimo datagramma arriva all’ n-esimo router:
- Il router scarta il datagramma.
- Invia all’origine un messaggio di allerta ICMP (tipo 11, codice 0).
- Il messaggio include il nome del router e l’indirizzo IP.

Quando il messaggio ICMP arriva all'host che ha avviato il programma `tracerout`, è possibile calcolare il RTT (Round-Trip Time).

![[Pasted image 20250510162114.png|600]]