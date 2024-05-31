---
created: 2023-10-29
type: Uni Note
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
academic year: 2023/2024
related:
  - "[[Circuiti combinatori]]"
completed: true
updated: 2024-05-27T13:29
---
---
## Index
1. [[#Definizione]]
2. [[#Calcolo numero variabili]]
3. [[#Circuito interno]]
4. [[#MUX Tree]]

---
## Definizione

É un circuito combinatorio che seleziona uno dei segnali binari in input e li dirige in una sola uscita

>[!warning] Rappresentazione circuitale
>![[Pasted image 20240202103619.png|350]]

**Utilizzi:**
1. Ridurre numero di linee
2. Riduzione complessità e costo di un circuito
3. Implementazione di altri circuiti (es: [[Half-Adder]], [[Full-Adder]])

---
## Calcolo numero variabili 

*Input* = n
*Output* = 1
*Selection* = $\log_{2}n$

---
## Circuito interno
- Insieme di porte [[Operatori Booleani e Porte Logiche#AND|AND]] che confluiscono in una porta [[Operatori Booleani e Porte Logiche#OR|OR]] 

>[!warning] MUX 2-1:
![[Pasted image 20240123113632.png|600]]

>[!warning] MUX 1-4:
>![[Pasted image 20240202105942.png|600]]
---

---
## MUX Tree

>[!tip] 
> È possibile unire due circuiti multiplexer tra loro per crearne uno più grande

![[Screenshot 2023-11-02 at 11.16.49.png|600]]

---