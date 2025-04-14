---
type: Uni Note
class: "[[Reti (class)]]"
academic year: 2024/2025
related: 
completed: false
created: 2025-04-13T16:12
updated: 2025-04-13T19:09
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
4. riceve `7001`, se arriva entro i `500 ms` allora `ACK cum 8001`, altrimenti `ACK post 8001`
