---
created: 2024-02-04
type: Uni Note
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
academic year: 2023/2024
related:
  - "[[Circuiti Aritmetici]]"
  - "[[Circuiti combinatori]]"
completed: true
updated: 2026-01-31T13:32
---
 >[!abstract] Index
>1. [[#Introduzione]]
>2. [[#Circuito Sottrattore]]
>3. [[#Circuito somma e sottrazione]]

>[!abstract] Related
>- [[Ripple Carry Adder]]
>- [[Circuiti Aritmetici]]
>- [[Circuiti combinatori]]
>- [](Circuiti%20combinatori.md)Digitali (class)]]

---
## Introduzione

Come vedremo il [[Ripple Carry Adder]] per effettuare la sottrazione utilizzerà l'codifica [[Codifica complemento a due (CA2)|CA2]],

Quindi la sottrazione di due numeri non è altro che la somma del primo con il [[Codifica complemento a due (CA2)#Conversione (metodo circuitale)|complemento ca2]] del secondo.

- $A-B = A - \overline{B} +1$

>[!warning] Complemento CA2?
>Per **complementare** un numero in **CA2** serve: 
>- Negare tutti i singoli bit che compongono il numero
>- Sommare 1

---
## Circuito Sottrattore

Il [[Ripple Carry Adder]] può essere implementato per effettuare la sottrazione effettuando le stesse operazioni del [[Ripple Carry Adder]] ma:
- Negando ogni bit di `b` 
- E dopo aver effettuato la somma, basta somma il risultato con `1` per ottenere il giusto risultato in  [[Codifica complemento a due (CA2)|codifica CA2"]]

>[!danger] Problema (ritardo)
>Il ripple carry adder, tuttavia, da il risultato dopo n cicli, poiché il [[Full-Adder]] deve aspettare il riporto del FA precedente. 
>
>Perciò eseguire un' ulteriore somma raddoppierebbe il costo dal punto di vista temporale.
>
>Per risolvere questa situazione, l'Half adder viene sostituito da un Full adder con riporto di ingresso pari a 1

>[!warning] Circuito
>![[Pasted image 20240204192753.png|700]]

---
## Circuito somma e sottrazione

Le due operazioni possono essere combinate in un unico circuito attraverso un sistema di selezione formate da porte [[Operatori Booleani e Porte Logiche#XOR|XOR]] connesse agli ingressi del secondo addendo (`b`). Il segnale di selezione (sel) controlla l'operazione da eseguire: 
- **sel = 0** --> il circuito opera da sommatore.
- **sel = 1** --> il circuito opera da sottrattore.

>[!warning] Circuito
>![[Pasted image 20240204192820.png|700]]

>[!warning] Funzionamento
>![[Pasted image 20240204172818.png|400]]
>- Quando **Sel = 0** il circuito è in modalità **somma**, infatti i bit di B non vengono commentati e il primo full-adder riceve *zero* come *carry*.
>- Quando **Sel = 1** il circuito è in modalità **sottrazione**, infatti i bit di B vengono commentati e il primo full-adder riceve *uno* come *carry* 
