---
created: 2023-10-29
type: Uni Note
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
academic year: 2023/2024
related:
  - "[[Circuiti combinatori]]"
completed: true
updated: 2024-11-18T20:21
---
>[!abstract] Index
>1. [[#Introduzione]]
>3. [[#Circuito]]
>4. [[#MUX Tree]]

>[!abstract] Related
>- [[Circuiti combinatori]]
>- [[Circuito De-multiplexer]]
>- [[Progettazione Sistemi Digitali (class)]]

---
## Introduzione

É un circuito combinatorio che seleziona uno dei segnali binari in input e li dirige in una sola uscita

>[!note] Rappresentazione circuitale
>![[Pasted image 20240202103619.png|350]]

>[!note] Input / Output 
>- *Input* = n
>- *Output* = 1
>- *Selection* = $\log_{2}n$

>[!warning] Utilizzi
>1. Ridurre numero di linee
>2. Riduzione complessità e costo di un circuito
>3. Implementazione di altri circuiti (es: [[Half-Adder]], [[Full-Adder]])

---
## Circuito

>**OSS:** Il circuito è un insieme di porte [[Operatori Booleani e Porte Logiche#AND|AND]] che confluiscono in una porta [[Operatori Booleani e Porte Logiche#OR|OR]] 

>[!warning] MUX 2-1:
>![[Pasted image 20240123113632.png|600]]

>[!warning] MUX 4-1:
>![[Pasted image 20240202105942.png|600]]

---
## MUX Tree

>[!tip] 
> È possibile unire due circuiti multiplexer tra loro per crearne uno più grande.

![[Screenshot 2023-11-02 at 11.16.49.png|600]]
