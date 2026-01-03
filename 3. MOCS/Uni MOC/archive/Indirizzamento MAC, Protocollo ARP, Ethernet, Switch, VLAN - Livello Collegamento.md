---
type: Uni Note
class: "[[Reti (class)]]"
academic year: 2024/2025
related: 
completed: true
created: 2025-06-12T13:13
updated: 2025-06-14T16:27
---
## Indirizzi MAC

Gli **indirizzi IP** sono utilizzati nel [[Introduzione al Livello di Rete|Livello di rete]] per individuare i punti di Internet dove sono connessi gli host sorgente e destinazione.

Quando un datagramma[^1] passa dal livello di rete al livello al livello di collegamento, viene incapsulato in un frame[^2] con intestazione che contiene gli **indirizzi MAC** della sorgente e destinazione del frame (non del datagramma).

Un indirizzo MAC è composto da `48 bit`, ovvero 6 byte rappresentati in esadecimale.

Ogni ***scheda di rete*** ha un indirizzo MAC **univoco**. Per questo quando una società vuole costruire degli adattatori deve comprare un blocco di indirizzi alla IEEE[^3].
-  **portabilità** -> è possibile spostare una scheda LAN da una LAN a un’altra

Come vengono determinati gli indirizzi di collegamento dalla sorgente alla destinazione? Con **[[#Address Resolution Protocol (ARP)|Address Resolution Protocol (ARP)]]**.

## Address Resolution Protocol (ARP)

Lo scopo di questo protocollo è quello di determinare l'indirizzo MAC di un interfaccia conoscendo soltanto l’indirizzo IP.

Ogni nodo IP (host o router) nella LAN ha una tabella ARP che contiene la corrispondenza tra indirizzi IP e MAC in dei record con il seguente formato:

```
<Indirizzo IP; Indirizzo MAC; TTL>
```
- Il ***TTL*** indica il Time To Live ovvero quando eliminare quella voce dalla tabella.

**Esempio:**

![[Pasted image 20250614111545.png|700]]

>[!note] Riempimento Tabella
>
>Cosa succede se `A` vuole inviare un datagramma a `B` senza avere il suo indirizzo MAC nella sua tabella?
>
>Viene inviato un pacchetto **broadcast** di richiesta ARP contenente l’indirizzo IP di `B`.
>
>In questo modo tutti i nodi della rete ricevono il pacchetto di richiesta ARP ma soltanto il nodo con l’indirizzo IP specificato risponde, quindi in questo caso `B` *risponde* ad `A` comunicandogli il proprio indirizzo MAC.
>
>**Protocollo Plug-and-Play:** La tabella ARP di un nodo si costruisce automaticamente e non c’è quindi bisogno di un intervento da parte dell’amministratore di sistema.

>[!note] Formato Pacchetti ARP
>
>![[Pasted image 20250614113440.png|600]]
>
>I pacchetti ARP sono incapsulati direttamente all’interno di un frame di livello di collegamento:
>
>![[Pasted image 20250614113505.png|600]]

### Indirizzamento

Come avviene l’invio di dati verso un nodo esterno alla sottorete?

![[Pasted image 20250614114016.png|700]]

Grafico del flusso di pacchetti che avviene nella sorgente (A):

![[Pasted image 20250614114106.png|700]]

1. Il livello applicazione richiede al DNS l’indirizzo IP di Gabriele. La richiesta viene quindi passata al livello di trasporto e incapsulata in un segmento.
2. Il segmento arriva al livello di rete; qui si individua il prossimo hop consultando la tabella di inoltro. Quindi, grazie all’ARP, si ottiene l’indirizzo MAC corrispondente all’indirizzo IP di destinazione.
3. Il segmento viene incapsulato in un datagramma IP.
4. Il datagramma IP viene a sua volta incapsulato in un frame a livello di collegamento.
5. Infine, il frame viene trasmesso al livello fisico.

Cosa accade invece nel Router R1?

![[Pasted image 20250614114626.png|700]]

Dobbiamo risalire lo stack fino al livello di rete:

1. Al livello fisico riceviamo il frame, ne estraiamo i due indirizzi MAC e lo decapsuliamo. Otterremo così il datagramma, che viene passato al livello di collegamento.
2. Dal datagramma ricaviamo l’indirizzo IP di destinazione e, consultando la tabella di inoltro, individuiamo il prossimo indirizzo IP. Quindi utilizziamo ARP per tradurre quell’indirizzo IP in un indirizzo MAC di collegamento, che impiegheremo per costruire il nuovo frame.

Flusso di pacchetti alla destinazione B:

![[Pasted image 20250614115047.png|350]]

Dobbiamo semplicemente risalire lo stack fino a ricavare la richiesta del livello applicazione.

## IEEE 802

Nel 1985 la IEEE Computer Society avviò il “**Progetto 802**” con l’obiettivo di definire uno standard di interconnessione tra dispositivi di produttori diversi.  
In particolare, il lavoro si concentrò sulla specifica delle funzioni dei livelli fisico e di collegamento per le reti LAN.

Il risultato di questo sforzo fu lo standard **IEEE 802**.

>[!note] IEEE 802
>
>IEEE ha proposto diversi standard per le LAN, questi includono gli standard per:
>- *Specifiche generali del progetto* - 802.1
>- *Logical Link Control LLC* - 802.2 (rilevazione errori, controllo flusso, parte del framing)
>- *CSMA / CD* - 802.3
>- *Token bus* - 802.4, destinato a LAN per automazione industriale
>- *Token ring* - 802.5
>- *DQDB* - 802.6, destinato alle MAN
>- *WLAN* - 802.11

## LAN cablate: Ethernet

È stata la prima LAN ad *alta velocità* ed ancora oggi è la più diffusa, la sua dominanza e dovuta da:
- **Semplice ed economica:** Più semplice e meno costosa di altre reti LAN come token ring, FDDI e ATM.
- **Aggiornata:** il tasso trasmissivo inizialmente era 10 Mbps ([[#Ethernet Standard (10 Mbps)|Ethernet Standard]]) ora arriva anche a 10 Gbps (10 Gigabit Ethernet).

### Ethernet Standard (10 Mbps)

I frame utilizzati nel Ethernet Standard hanno questo formato:
 
![[Pasted image 20250614121532.png|900]]

- **Preambolo** - Attiva le NIC[^4] dei riceventi e sincronizza i loro orologi con quello del trasmittente.
- **SFD (Start Frame Delimeter)** - Flag che definisce l’inizio del frame, gli ultimi due bit indicano che inizia l’header.
- **Indirizzi sorgente e destinazione** - Indirizzo MAC della destinazione e della sorgente (ovvero del NIC).
- **Tipo** - Indica  il protocollo di livello superiore del pacchetto incapsulato nel frame (IP, ARP, OSPF, etc.).
- **Dati** - Contiene un datagramma del livello di rete. Se il campo è più piccolo di 46byte viene riempito di 0 fino a raggiungere la dimensione (padding).
- **CRC** - Consente alla NIC di rilevare la presenza di un errore nei bit sui campi indirizzo, tipo e dati.

>[!bug] Criticità
>
>- **Senza connessione**: non è prevista nessuna forma di handshake preventiva con il destinatario prima di inviare un pacchetto.
>- **Non affidabile** (come IP e UDP): la NIC ricevente non invia un riscontro.

>[!note] Indirizzi Ethernet
>
>Tutte le stazioni che fanno parte di una LAN Ethernet sono dotate di una Network Interface Card (NIC), ossia la scheda di rete. La NIC fornisce l’indirizzo di collegamento (indirizzo MAC).  
>
>Nella trasmissione, i byte vengono inviati da sinistra verso destra, tuttavia, all’interno di ciascun byte il bit meno significativo (LSB) viene trasmesso per primo, mentre il bit più significativo (MSB) per ultimo.

### Protocollo CSMA/CD di Ethernet

Le **fasi operative** del protocollo [[Protocolli del Livello Collegamento#CSMA/CD (collision detection)|CSMA/CD]] di Ethernet sono:
1. **Framing** - Il NIC riceve un datagramma di rete dal nodo a cui è collegato e prepara un frame ethernet.
2. **Carrier Sense e Trasmissione** - Se il canale è inattivo (lo si capisce vedendo il livello di energia sul mezzo trasmissivo) inizia la trasmissione, se invece risulta occupato allora si resta in attesa fino a quando non è inattivo.
3. **Collision Detection** - Verifica, durante la trasmissione, la presenza di segnali provenienti da altri NIC, se non ci sono allora il pacchetto viene spedito.
4. **Jamming** - Se vengono rilevati segnali da altri NIC interrompe la trasmissione del pacchetto e invia un segnale di disturbo ([[#^41f27d|jam]]).
5. **Backoff Esponenziale** - Il NIC rimane in attesa, quando riscontra la n-esima collisione consecutiva stabilisce un valore `k` tra ${0,1,2,…,2^{m}−1}$ dove m è il minimo tra `n` e `10`. La NIC aspetta un tempo pari a k volte `512 bit` e ritorna la Passo 2 (carrier sense).

>[!note] Segnale Jam
>
>Il segale di disturbo (jam) è composto da 48 bit e il suo obiettivo è quello di avvisare della collisione tutte le altre NIC che sono in fase trasmissiva.

^41f27d

### Fast Ethernet (100 Mbps)

Negli anni 90 [[#Ethernet Standard (10 Mbps)|Ethernet Standard]] si è evoluta a Fast Ethernet (100 Mbps) mantenendo compatibilità con la versione precedente.

>[!bug] Problema Compatibilità
>
>Per garantire il corretto funzionamento del CSMA/CD e mantenere una durata minima del frame di 512 bit, è necessario *ridurre proporzionalmente la lunghezza massima* della rete. 
>
>Infatti, se la velocità di trasmissione aumenta di 10 volte, anche il tempo di trasmissione di un frame da 512 bit diventa 10 volte più breve: di conseguenza, le collisioni devono essere rilevate 10 volte più rapidamente. 
>
>Per rispettare questa condizione, la rete deve quindi essere 10 volte più corta.
>
>Sono state implementate due soluzioni al problema: [[#Soluzione 1 (Hub)]], [[#Soluzione 2 (Switch)]].

#### Soluzione 1 (Hub)

Abbandonare la topologia a stella e utilizzare un hub passivo e fissare la dimensione massima della rete a 250 metri invece che 2500.

![[Pasted image 20250614144954.png|450]]

L’**hub** è un dispositivo che *opera a livello fisico* sui singoli bit:
- All’arrivo di un bit, l’hub lo rigenera aumentando il livello di segnale e lo inoltra simultaneamente su tutte le altre porte.
- Non implementa né rilevazione della portante né CSMA/CD.
- Ripete il bit in entrata su tutte le interfacce uscenti, anche se su alcune di esse è già presente un segnale.
- Trasmette in broadcast: ogni NIC può quindi sondare il canale per verificarne lo stato e rilevare eventuali collisioni durante la trasmissione.

#### Soluzione 2 (Switch)

Si utilizza uno [[#Switch Ethernet]] di collegamento dotato di buffer per memorizzare i frame e offre connessioni full-duplex verso ciascun host.

- Ogni host dispone di un mezzo trasmissivo dedicato e privato, perciò non è più necessario utilizzare CSMA/CD: non c’è più competizione sul canale.
- Lo switch riceve un frame da un host, lo memorizza nel buffer, ne legge l’indirizzo di destinazione e lo inoltra sull’interfaccia appropriata.
- In pratica, il singolo mezzo condiviso è stato sostituito da più collegamenti punto-punto.

**Vantaggio:** Lo switch quindi consente più trasmissioni simultanee senza collisioni.

![[Pasted image 20250614151357.png|700]]

## Switch Ethernet

Lo switch è un dispositivo del livello di collegamento più “intelligente” di un hub e **opera in modo attivo**:  
- Filtra e inoltra i frame Ethernet.  
- Esamina l’indirizzo di destinazione e invia il frame sull’interfaccia corrispondente.  
- È trasparente: gli host non sono consapevoli della sua presenza.

>[!note] Proprietà
>
>- Sono dispositivi “plug-and-play”, ovvero non richiedono configurazioni da parte dell’amministratore di rete.  
>- Eliminano le collisioni grazie al buffering dei frame.  
>- Interconnettono link eterogenei, ovvero con velocità di trasmissione differenti.  
>- Aumentano la sicurezza della rete e migliorano il network management.

>[!note] Auto apprendimento
>
>All’inizio gli switch erano configurati staticamente, ma oggi adottano un meccanismo dinamico di auto-apprendimento. Anche senza alcuna configurazione preventiva, sono in grado di costruire una tabella di commutazione che associa indirizzi MAC alle rispettive interfacce.
>
>Quando lo switch riceve un frame:
> 1. Esamina l’indirizzo MAC sorgente.
>2. Se nella tabella di commutazione non esiste ancora una voce per quell’indirizzo, lo switch la crea, registrando l’indirizzo MAC e l’interfaccia di arrivo.
>3. Se l’indirizzo MAC sorgente è già presente, lo switch aggiorna eventualmente la voce con la nuova interfaccia e TTL
>   
>Quando deve inoltrare un frame, lo switch segue due possibili percorsi:
>- Se l’indirizzo di destinazione non è presente nella tabella di commutazione, il frame viene **floodato**, cioè trasmesso su tutte le porte tranne quella di arrivo.
>- Se l’indirizzo di destinazione è noto, il frame viene inviato **soltanto** sull’interfaccia corrispondente.
>
>In questo modo lo switch “apprende” dinamicamente quali nodi sono raggiungibili attraverso ciascuna porta, migliorando l’efficienza nell’inoltro dei frame.
>
>![[Pasted image 20250614152651.png|600]]

## Virtual Lan (VLAN)

Supponiamo di avere uno switch che collega 3 LAN, ognuna associata ad un gruppo di lavoro. 

- Cosa succede se una persona del primo gruppo viene spostata?
- Se avessimo 10 gruppi composti da poche persone, avremmo bisogno di 10 switch?

![[Pasted image 20250614153605.png|600]]

Le VLAN risolvono questi problemi: sono reti locali definite via software anziché tramite cablaggio fisico. Invece di separare gli host in base alla loro collocazione fisica, una LAN può essere suddivisa in più segmenti logici.

La creazione delle VLAN avviene via software, assegnando a ciascuna porta dello switch una VLAN specifica. Ne deriva una tabella di associazione “VLAN ↔ interfaccia”.

![[Pasted image 20250614153950.png|600]]

>[!note] Switch Virtuali
>
>Se uno switch supporta le VLAN, lo si può considerare come più switch “virtuali” riuniti in un unico dispositivo.
>
>![[Pasted image 20250614154040.png|500]]

>[!note] VLAN Trunking
>
>Quando un gruppo di lavoro è distribuito su più aree, si utilizza il VLAN Trunking:  
>- Si configura su ogni switch una porta speciale (trunk) dedicata all’interconnessione con gli altri switch.  
>- Questa porta trunk appartiene simultaneamente a tutte le VLAN e trasporta i frame relativi a ciascuna di esse, contrassegnandoli opportunamente.
>  
>![[Pasted image 20250614154537.png|700]]
>
>Quindi è come “condividere” la tabella VLAN su più switch.

[^1]: nome del "pacchetto" nel livello di rete.

[^2]: nome del "pacchetto" nel livello di collegamento.

[^3]: IEEE: Institute of Electrical and Electronics Engineers, è un organizzazione che tra le tante cose sovrintende alla gestione e assegnazione degli indirizzi MAC.

[^4]: NIC: Network Interface Card
