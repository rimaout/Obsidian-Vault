---
type: Uni Note
class: "[[Reti (class)]]"
academic year: 2024/2025
related: 
completed: false
created: 2025-04-13T16:12
updated: 2025-04-14T18:32
---
## Esercizio 1

In una rete con un valore fisso `m > 1`, è possibile utilizzare entrambi i meccanismi Go-Back-N e Selective-Repeat.

**Domanda 1:** Indicare i vantaggi e gli svantaggi dell’impiego di ciascuno di essi.

**Domanda 2:** Quali altre considerazioni si devono fare per decidere quale meccanismo utilizzare?

![[Pasted image 20250413184454.png|1000]]

## Esercizio 2

Un server TCP ha ricevuto e riscontrato all’interno di una connessione i byte
fino al 4000. Dire quale azione esegue il server dopo i seguenti eventi:
1. Il server riceve un segmento di 1000 byte con numero di sequenza pari a 3001
2. In seguito all’evento 1 il server riceve un segmento di 1000 byte con numero di sequenza pari a 6001
3. In seguito all’evento 2 il server riceve un segmento di 1000 byte con numero di sequenza pari a 5001
4. In seguito all’evento 3 il server riceve un segmento di 1000 byte con numero di sequenza pari a 4001

**Risposta:**
1. riceve `3001`, invia `ACK dup 4001`
2. riceve `6001`, invia `ACK dup 4001`
3. riceve `5001`, invia `ACK dup 4001`
4. riceve `4001`, invia `ACK cum 7001`

## Esercizio 3

Un server TCP ha ricevuto e riscontrato all’interno di una connessione i byte fino al 4000. Dire quale azione esegue il server dopo i seguenti eventi:
1. Il server riceve un segmento di 1000 byte con numero di sequenza pari a 5001
2. In seguito all’evento 1 il server riceve un segmento di 1000 byte con numero di sequenza pari a 4001
3. In seguito all’evento 2 il server riceve un segmento di 1000 byte con numero di sequenza pari a 6001
4. In seguito all’evento 3 il server riceve un segmento di 1000 byte con numero di sequenza pari a 7001

delay = 500ms

**Risposta:**
1. riceve `5001`, invia `ACK dup 4001` 
2. riceve `4001`, invia `ACK cum 6001`
3. riceve `6001`, aspettiamo `500ms` ma non arriva `7001` quindi inviamo `ACK post 7001`
4. riceve `7001`, se entro `500 ms` arriva sequenza `8001` allora `ACK cum 9001`, altrimenti `ACK post 8001`

## Esercizio 4

**Domanda:** Nel protocollo TCP la finestra di invio può essere più piccola, più
grande o della stessa dimensione della finestra di ricezione?

![[Pasted image 20250414112713.png|800]]

## Esercizio 5

**Domanda:** L’utente A utilizza il proprio browser per aprire due connessioni con il
server HTTP in esecuzione sull’host B. Come può il protocollo TCP distinguere queste due connessioni?

![[Pasted image 20250414112925.png|800]]

## Esercizio 6

In una rete basata su Go-Back-N con `m=3` e dimensione della finestra
di invio uguale a `7`, i valori delle variabili sono: `Sf=62`, `Sn=66` e `Rn=64`. 

Si ipotizzi che la rete non duplichi e non alteri l’ordine dei pacchetti.
1. Qual è il numero di sequenza dei pacchetti in transito?
2. Qual è il numero di riscontro dei pacchetti ack in transito?

**Riposta:**
- Sono stati inviati 62 63 64 65 ma ancora non è stato ricevuto il riscontro
- Gli ack in transito sono di 62 e 63

![[Pasted image 20250414120907.png|600]]


## Esercizio 7

**Domanda:** Si può definire il prodotto rate-ritardo come il numero di pacchetti che possono essere in transito nella rete durante un tempo pari a RTT.

Calcolare il prodotto rate-ritardo nel caso in cui:
- $\text{Rate} = 1 \text{ Mbps} = 10^{6} \frac{\text{bit}}{s}$
- $\text{RTT} = 20\text{ ms} = 20 \cdot 10^{-3} \text{ s}$
- $\text{Dimensione dei pacchetti} = 1000 \text{ bit} = 10^{3} \text{ bit}$

**Risposta Mia:** 

$$
\begin{align*}
 & - \ \ \text{TP}= \text{Tempo per spedire un pachetto} = \frac{10^{3}}{10^{6}} \frac{\text{bit}}{\frac{\text{bit}}{\text{s}}} = 10^{-3} \text{s}\\
 & - \text{Rate-Ritardo} = \frac{\text{RTT}}{TP} = \frac{20 \cdot  10^{-3}}{10^{-3}} = 20
\end{align*}
$$

**Risposta Prof:**

$$
\begin{align*}
& - \ \ \text{BDP} = 1 \text{ Mbps} \cdot 20 \text{ ms} = 20000 \text{ bit} \\
& - \ \ \text{rate-ritardo} = 20000 \text{ bit } / 1000 \text{ bit} = 20 \text{ pacchetti}
\end{align*}
$$

## Esercizio 8

- $\text{Rate} = 1 \text{ Gbps} = 10^{9} \text{ bps}$
- $D = 50000 \text{ bit} = 5 \cdot 10^{4} \text{ bit}$
- $\text{Distanza} = 5000 \text{ km} = 5 \cdot 10^{6} \text{ m}$
- $V_{\text{Propagazione}} = 2 \cdot 10^{8} \text{ m/s}$

Vogliamo calcolare il numero di pacchetti che possono essere nella rete in un determinato istante, per fare ciò calcoliamo il `rate-ritardo` che rappresenta il numero di bit massimo nella rete in un determinato istante e poi da esso possiamo ottenere il numero di pacchetti massimo possibile nella rete.

- $\text{Ritardo Propagazione} = \frac{\text{Distanza}}{V_{\text{Propagazione}}} = \frac{5 \cdot 10^{6} \text{ m}}{2 \cdot 10^{8} \frac{m}{s}} = \frac{5}{2} \cdot 10^{-2}\text{ s}$
- $\text{RTT} = \text{Ritardo Propagazione} \cdot 2 = 2 \cdot \frac{5}{2} \cdot 10^{-2} \text{ s}$

Con `rate-ritardo` otteniamo il numero di bit massimo nella rete in un determinato istante:
$$
\text{rate-ritardo} = 10^{9}\cdot 5 \cdot 10^{-2} = 5 \cdot  10^{7} bit
$$

Ora possiamo calcolare il numero massimo di pacchetti:
$$
\frac{\text{rate-ritardo}}{D} = \frac{5 \cdot  10^{7}}{5 \cdot 10^{4}} = 10^{3} \text{ pachetti}
$$

Quindi la dimensione massima della finestra di invio quindi deve essere di 1000 pacchetti ($10^{3}$), questo perché non possiamo inviare più pacchetti di quelli supportati dalla rete.

>***oss:*** in selective repeat la finestra non deve superate $2^{m-1}$, invece in go back n non deve superate $2^{m}-1$.

Quindi abbiamo finestra da `1000`, quindi dobbiamo trovare un `m` tale che $2^{m-1}$ sia il più piccolo numero superiore a `1000`.
- Per ottenere ciò pendiamo `m = 11` infatti $2^{11 - 1} = 2^{10} = 1024$ 
- I numeri di sequenza vanno da $0$ a $2^{m}-1$ ovvero da `0` a `2047` ($2^{11}-1$).

>[!note] Scala grandezze
>- Pico = $10^{-12}$
>- Nano = $10^{-9}$
>- Micro = $10^{-6}$
>- Milli = $10^{-3}$
>---
>- Kilo = $10^{3}$
>- Mega = $10^6$
>- Giga = $10^{9}$
>- Tera = $10^{12}$



**Timeout:**
- SlowStart
- Tr = cwnd/2    
- Cwnd = 1


**3ACK:**
- FastRecovery
- Tr = cwnd/2
- cwnd = tr + 3

