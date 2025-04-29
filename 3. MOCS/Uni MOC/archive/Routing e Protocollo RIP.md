---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-04-24T14:15
updated: 2025-04-24T15:20
---
Vedremo in questo momento routing intra-dominio, ovvero routing che avvengono in una rette gestita completamente da uno stesso service provider, asd esempio la rete del gar.

## Routing Intra dominio

Quando si parala di routing la rete va vista come un grafo `G` dove:
- I nodi rappresentano i router
- Gli archi rappresentano i collegamenti (link) tra i nodi.

Solitamente si utilizzano grafi pesati, dove il peso può rappresentare un costo, ad esempio tempo di percorrenza, congestione o costo monetario.

>[!note] Algoritmo di Instradamento
>
>Determina il cammino che collega due nodi con costo minimo.

^4badd5

## Algoritmo d’instradamento con vettore distanza (Distance Vector - DV)

Questo è [[#^4badd5|algoritmo di instradamento]] che utilizza l'*Equazione di Bellman-Ford* e il concetto di *vettore delle distanze* ed ha queste due caratteristiche:
- **Distribuito** - ogni nodo riceve informazione dai vicini e opera su quelle
- **Asincrono** - non richiede che tutti i nodi operino al passo con gli altri

## Protocollo RIP (Routing Information Protocol)

Il protocollo RIP è l’implementazione del algoritmo appena visto.

Questo protocollo non è utilizzabile su reti di gradi dimensione dove il numero di salti non è maggiore di 15, questo perché richiede che i router comunichino tra di loro.

### Messaggi rip

RIP si basa su una coppia di processi client-server e sul loro scambio di messaggi

RIP Request:
- Quando un nuovo router viene inserito nella rete invia una RIP Request per ricevere immediatamente informazioni di routing
- Fini diagnostici (richiedere una voce specifica)

RIP Response (o advertisements):
- In risposta a una Request (solicited response)
- Peridiocamente ogni 30 sec (unsolicited response)

Ogni messaggio contiene un elenco comprendente fino a 25 sottoreti di destinazione all’interno del sistema autonomo nonché la distanza del mittente rispetto a ciascuna di tali sottoreti.

>[!note] Struttura messaggi
>
>![[Screenshot 2025-04-24 at 15.15.26.png|650]]
>
>- *Com*: comando, richiesta(1), risposta (2)
>- *Ver*: versione, la versione corrente è 2
>- *Family*: famiglia del protocollo, per il TCP/IP il valore è 2
>- *Tag*: informazioni sul sistema autonomo
>- *Network address*: indirizzo di destinazione
>- *Subnet mask*: maschera di sottorete (lunghezza del prefisso)
>- *Next-hop address*: indirizzo del prossimo hop
>- *Distance*: numero di hop fino alla destinazione

### Timer 