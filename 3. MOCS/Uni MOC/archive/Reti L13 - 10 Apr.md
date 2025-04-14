---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-04-10T14:16
updated: 2025-04-10T15:20
---
## Indirizzamento IPV4

Ogni interfaccia di host e router di Internet ha un indirizzo IP. Un interfaccia ....

**Indirizzo IP:** 32 bit (4 byte) in notazione decimale puntata (ciascun byte dell’indirizzo viene indicato in forma decimale)

>[!note] Notazione Indirizzi


Esistono due modi per effettuare indirizzamento:
- [[#Indirizza per classi]]
- [[#Indirizzamento senza classi]]

## Indirizza per classi



## Indirizzamento senza classi


## Indirizzi Speciali



## DHCP Esempio

![[Pasted image 20250410145130.png|600]]

IL client
- Abbiamo una macchina che si conette ad una rete e ne rixhiede un indirizzo IP.
- Non sa chi è il sever DHCP o il server DNS, quindi fa una richiesta brodcast diretta a tutti i nodi della rede (255.255.255.255), ma non avendo un indirizzo ip come suource addres mette tutti 0

Il server DHCP:
- una volta ricevuta la richiesta invia una risposta contenete l'addres da assegnare al client (in questo caso: 181.14.16.182) anche queta risposta viene mandata in brodcast  (255.255.255.255) a tutti i nodi della rede visto che il client che ha effettutato la richiesta non conosce ancora il suo indirizzo IP.

Il client:
- Il client riceve il suo indirizzo IP e invia la conferma di ricevimento, ma questa risposta non viene mandata a tutti i nodi della rete (brodacat) e non solo al serve che gli ha assegnato l'indirizzo IP. Queso perche in una rete possono esserci più server DHCP e quindi ognuno di questo avevva generato precedentemente un indirizzo il per il client quando aveva effettuato la richiesta, il client utilizza come indirizzo IP il primo che riceva ma deve notificare tutti gli altri server DHCP un modo tale che sappiano che l'indirizzoindirzzo IP da loro generato non è stato utilizzato e che quindi potrà essere utilizzato per qualche altro dispositivo.

---
## Forwarding Datagrammi IP

