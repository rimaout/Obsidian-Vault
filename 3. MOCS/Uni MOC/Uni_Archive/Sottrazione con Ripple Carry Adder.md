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
updated: 2024-05-27T13:29
---
---
## Sottrazione in CA2

In [[Codifica complemento a due (CA2)|CA2]] la sottrazione di due numeri non è altro che la somma del primo con il [[Codifica complemento a due (CA2)#Conversione (metodo circuitale)|complemento]] del secondo 

- $A-B = A - \overline{B} +1$

>[!warning] oss
>**Complemento in CA2** è uguale alla negazione di tutti i singoli bit e la somma di 1

---
## Circuito sottrazione

Il [[Ripple Carry Adder]] può essere implementato per effettuare la sottrazione basta negare ogni bit di b e dopo aver effettuato la somma sommare sommare anche 1

Il ripple carry adder, tuttavia, da il risultato dopo n cicli, poiché il [[Full-Adder]] deve aspettare il riporto del FA precedente. Perciò eseguire un' ulteriore somma raddoppierebbe il costo dal punto di vista temporale.

Per risolvere questa situazione l'Half adder viene sostituito da un Full adder con riporto di ingresso pari a 1

>[!warning] Circuito
>![[Pasted image 20240204192753.png|700]]

---
## Circuito somme e sottrazione
Le due operazioni possono essere combinate in un unico circuito attraverso un sistema di selezione formate da porte XOR connesse agli ingressi del secondo addendo (b). Il segnale di selezione (sel) controlla l'operazione da eseguire: 
- **sel = 0** --> il circuito opera da sommatore.
- **sel = 1** --> il circuito opera da sottrattore.

>[!warning] Circuito
>![[Pasted image 20240204192820.png|700]]

>[!warning] Funzionamento
>![[Pasted image 20240204172818.png|400]]
>- Quando **Sel = 0** il circuito è in modalità **somma**, infatti i bit di B non vengono commentati e il primo full-adder riceve *zero* come *carry*.
>- Quando **Sel = 1** il circuito è in modalità **sottrazione**, infatti i bit di B vengono commentati e il primo full-adder riceve *uno* come *carry* 

---