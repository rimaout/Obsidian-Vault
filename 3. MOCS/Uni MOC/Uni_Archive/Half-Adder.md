---
created: 2024-02-03
type: Uni Note
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
academic year: 2023/2024
related:
  - "[[Circuiti Combinatori]]"
  - "[[Circuiti Aritmetici]]"
completed: true
updated: 2024-06-12T16:24
---
---
## Index
1. [[#Definizione]]
2. [[#Circuito interno]]

---
## Definizione
**Half adder** è un [[Circuiti Combinatori|circuito combinatorio]] capace di effettuare somma tra due bit.

>[!warning] Rappresentazione circuitale
>![[Pasted image 20240203164534.png|200]]

>[!danger] I/0
**Input:**  Due bit *a* e *b* (addendi dell'operazione)
>
**Output:** 
>- *S* --> risultato della somma
>- *C* --> riporto della somma (carry)

---
## Circuito interno

>[!warning] Tavola di verità
>![[Pasted image 20240203170046.png|500]]

>[!warning] oss
>I valori assunti dal riporto `C` corrispondono a valori assunti dall'[[Operatori Booleani e Porte Logiche#AND|and]] tra gli ingressi, quindi:
>- $C = a \cdot b$ 
>
>I valori assunti dalla somma `S` corrispondono all'[[Operatori Booleani e Porte Logiche#XOR|xor]] tra gli ingressi, quindi:
>- $S = a \oplus b$

>[!warning] Circuito
>![[Pasted image 20240203171249.png|300]]

---