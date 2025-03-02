---
type: Uni Note
class:
  - "[[Reti (class)]]"
academic year: 2024/2025
related: 
completed: false
created: 2025-02-28T14:09
updated: 2025-02-28T15:23
---
## Access Network

## BackHome

Solo router e collegamenti tra router

## Livello Rete ISP

**Livello 1** es. gestiscono [[#Dorsali Sottomarine]]

**Livello 2**

**Livello 3**

L'azione di determinare il percorso di un pacchetto è chiamato routing

## Dorsali Sottomarine

![[Pasted image 20250228141445.png|800]]


# Fine Introduzioneeee 
[[Introduzione alle reti]]

---
# Capacità e prestazioni

sdakjhkjfahsdlkj

### Ampiezza di Banda (Rate)

Ci dice quanto il canale è capace di trasmettere concetto di base più è grande l'apliezza di banda maggiore è la quantità di informazione che può essere veicolata.

Con questa caratteristica si rappresentano due cose:

**Caratterizzazione del canale o del sistema trasmissivo** - 

**Caratterizzazione di un collegamento** - 



### Throughput

Il throughput indica quanto velocemente riusciamo ***effettivamente*** a inviare i dati tramite una rete.

Indica il numero di bit al secondo che passano attraverso un punto della rete.

Un link può avere un rate di `R` bps, ma possiamo inviare solo `T` bps (throughout) tramite
quel link, con `T ≤ R`.

>[!warning] Rate vs Throughput
>
>Il rate è una misura della potenziale velocità di un link, il throughput è una misura dell’effettiva velocità di un link (quanto velocemente riusciamo a inviare i dati in realtà)

>[!note] Bottleneck
>
>dhlkjghjkhkjshgkhdsfkj
>
>**oss:** solitamente il collo di bottiglia non è mai il backbone ma le reti di accesso.

>[!note] Throughput nei link condivisi
>
>ljkdsljafdlk
>
>![[Pasted image 20250228143551.png|800]]

### Delay e Loss dei Package

La **latenza (delay)** è quanto tempo necessario affinché un pacchetto arrivi completamente a destinazione dal momento in cui il primo bit parte dalla sorgente.

Se il tasso di arrivo dei pacchetti in un router è superiore al tasso di uscita allora i pachetti si accodano nei buffer di attesa.

Abbiamo 4 fattori che contribiscono ai ritardi:

**1. Ritardo di elaborazione del nodo (processing delay)** - 

**2. Ritardo di 

**3. Ritardo di **

**4. Ritardo di **

![[Pasted image 20250228144357.png|800]]

***rimuovi il giallo dalla foto:

**esempio macchine**

## Ritardo di accodamento

## Perdita di dati

## Trace Route

L’output presenta 6 colonne:
1. Il numero di router sulla rotta
2. Nome del router
3. Indirizzo del router
4. tempo di andata e ritorno 1° pacchetto
5. tempo di andata e ritorno 2° pacchetto
6. tempo di andata e ritorno 3° pacchetto

Tempo di andata e ritorno (*round trip time - RTT*) ed include i 4 ritardi visti precedentemete

