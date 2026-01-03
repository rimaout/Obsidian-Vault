---
type: Uni Note
class: "[[Reti (class)]]"
academic year: 2024/2025
related: 
completed: true
created: 2025-06-08T15:27
updated: 2025-06-08T18:55
---
## Unicast

Una comunicazione **unicast** avviene quando un pacchetto è inviato da un nodo sorgente ad un nodo destinazione.

Quindi abbiamo due informazioni:
- Indirizzo IP sorgente 
- Indirizzo IP destinazione

![[Pasted image 20250608154813.png|900]]

## Broadcast

Una comunicazione **broadcast** avviene quando un pacchetto è inviato da un nodo sorgente a **tutti** i nodi della rete.


Quindi abbiamo due informazioni:
- Indirizzo IP sorgente 
- Indirizzo IP broadcast

Esistono due principali metodi per effettuare un broadcast: [[#Uncontrolled Flooding]] e [[#Controlled flooding]].

#### Uncontrolled Flooding

Quando un nodo riceve un pacchetto broadcast, lo duplica e lo invia a tutti i nodi vicini (eccetto a quello da cui lo ha ricevuto).

>**Problema:** Se il grafo ha cicli, una o più copie del pacchetto cicleranno all’infinito nella rete.

#### Controlled flooding

>[!note] Sequence Number
>
>Consente di non forwardare pacchetti già ricevuti e inoltrati.
>
>Ogni nodo mantiene una lista dei pacchetti ricevuti e inoltrati, sotto forma di tuple `(indirizzo IP, #seq)`. Quando riceve un pacchetto controlla nella lista, se già inoltrato lo scarta, altrimenti lo forwarda.

>[!note] Reverse path forwarding (RPF)
>
>Il pacchetto in arrivo viene rispedito soltanto se è arrivato dal link che è sul suo shortest path (unicast) verso la sorgente.
>
>![[Pasted image 20250608163858.png|500]]
>
>- **Elimina** il problema di inondare la rete con troppi pacchetti.
>- **Non elimina** completamente il problema dei pacchetti ridondanti:
>	- Ad esempio B, C, D, E, F ricevono più pacchetti ridondanti
>	- Ogni nodo dovrebbe ricevere soltanto una copia del pacchetto broadcast
>
>Per risolvere questi problemi costruiamo lo **spanning tree** prima di inviare i pacchetti broadcast.

>[!note] Spanning Tree (center - based)
>
>Pre creare l'albero viene preso un nodo come centro, in questo caso `E`, ed ogni nodo invia un messaggio di join in unicast verso il centro, i messaggi vengono inoltrati finché:
>1. Arrivano ad un nodo che già appartiene all’albero
>2. Arrivano al centro
>
>![[Pasted image 20250608164539.png|900]]
>
>Facendo il broadcast sullo spanning tree si elimina il problema dei pacchetti duplicati.

## Multicast

Una comunicazione **multicast** avviene quando un pacchetto è inviato da una (o più) sorgente ad un gruppo di destinazioni.

>[!warning] Multicast != Unicast multiplo
>
>![[Pasted image 20250608165055.png|900]]

### Indirizzamento Multicast

L'obiettivo è comunicare con host che partecipano ad un gruppo (multicast) ma appartengono a reti diverse, però come sappiamo l’*indirizzo di destinazione* nell’IP può essere **uno solo**.

>**Soluzione**: unico indirizzo per tutto il gruppo, ovvero l'indirizzo multicast.

>[!note] Indirizzi Multicast
>
>Gli indirizzi multicast sono un range di indirizzi IP riservati proprio per questo scopo.
>
>In [[Internet Protocol v4 (IPv4) - Indirizzamento, DHCP, NAT, Forwarding|IPv4]] si è riservato il range da `224.0.0.0` a `239.255.255.255` infatti: `224.0.0.0/4`.
>
>In binario un indirizzo multicast ha questa struttura:
>- i primi 4 bit sono `1110`, che si ottengono prendendo i primi 4 bit di 11100000 (ovvero 224 in binario).
>- i restanti 28 bit sono "liberi" e vengono chiamati *identificatore del gruppo*
>  
>Quindi in totale esistono $2^{28}$ gruppi multicast possibili.

>[!note] Gruppi Multicast
>
>L’appartenenza ad un gruppo quindi non ha alcuna relazione con il prefisso associato alla rete. Ogni host che appartiene a un gruppo avrà infatti un indirizzo multicast separato e aggiunti rispetto a quello della rete.
>
>Come fa un router a sapere quali host appartengono a un gruppo? Il router deve scoprire quali gruppi sono presenti nelle sue interfacce e propagare questa informazioni agli altri router, per fare ciò si utilizza l'[[#Internet Group Management Protocol (IGMP)]].

### Internet Group Management Protocol (IGMP)

Lavora tra un host e il router collegato ad esso, permette appunto all’host di informare il router del fatto che un’applicazione vuole partecipare ad un gruppo multicast.

>[!note] Messaggi
>Questo protocollo invia messaggi incapsulati in datagrammi IP (con IP protocol number 2), vengono spediti con TTL (time to live) a 1. 
>
Ci sono diversi tipi di messaggi:
>- **Membership query** - Messaggio che va dal *router all’host* e serve a determinare a quali gruppi hanno aderito gli host su ogni interfaccia.
>- **Membership report** - Va da un *host al router* e serve ad informarlo sull’adesione ad un gruppo. Di solito vengono inviati in risposta ad una query ma non sempre
>- **Leave group** - Va da un *host al router* e si manda quando si lascia un gruppo, questi messaggi sono opzionali, il router infatti può capire che non ci sono più adesioni quando non riceve report in risposta ad una query.

>[!note] Membership Timer 
>
>Un router multicast tiene una lista per ciascuna sottorete dei gruppi multicast (**multicast group membership**) con un timer per membership:
>
>- Questa membership deve essere aggiornata con dei report prima dello scadere del timer
>- Può anche essere aggiornata tramite messaggi di leave espliciti

### Routing Multicast

Fra la popolazione complessiva di router solo i collegati a host del gruppo multicast dovranno ricevere traffico multicast.

Quindi è necessario utilizzare un protocollo che coordini i router multicast in Internet (instradare pacchetti multicast dalla sorgente alla destinazione).

![[Pasted image 20250608183150.png|800]]

Ci sono due diversi approcci per identificare questo albero:

>[!note] Albero condiviso dal gruppo
>
>Dal gruppo multicast viene scelto un router, che diventerà la radice/centro, e da questo viene generato un albero d'instradamento che raggiunge tutti i router del gruppo.
>
>Se il mittente del traffico multicast non è il centro dell'albero, allora esso invierà il traffico in unicast al centro, e il centro provvederà a inviarlo al gruppo, instrado seguendo l'albero.
>
>![[Pasted image 20250608185219.png|450]]

>[!note] Albero basato sull'origine
>
>Viene creato un albero per ciascuna origine nel gruppo multicast, quindi ci saranno tanti alberi quanti sono i mittenti del gruppo. 
>
>Per la costruzione degli alberi si usa un algoritmo basato su reverse path forwarding con pruning (potatura).
>
>![[Pasted image 20250608185400.png|450]]

### Instradamento Multicast in Internet

Si utilizzano i seguenti protocolli:

**Intra-dominio multicast** per istradamento interno a un sistema autonomo:
- *DVMRP*: distance-vector multicast routing protocol
- *MOSPF*: multicast open shortest path first
- *PIM*: protocol independent multicast

**Inter-dominio multicast** per istradare tra sistemi autonomi:
- *MBGP*: multicast border gateway protocol