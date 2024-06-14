---
created: 2024-02-03
type: Uni Note
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
academic year: 2023/2024
related:
  - "[[Circuiti Combinatori]]"
completed: true
updated: 2024-06-13T14:33
---
>[!abstract] Index
>1. [[#Introduzione]]
>2. [[#Circuito interno]]

>[!abstract] Related
>- [[Circuiti Combinatori]]
>- [[Operatori Booleani e Porte Logiche]]
>- [[Progettazione Sistemi Digitali (class)]]

---
## Introduzione

**Comparatore logico** confronta due sequenze di pit per verificarne l’uguaglianza.

>[!note] Rappresentazione circuitale
>![[Pasted image 20240203112236.png|250]]

>[!warning] Input / Output
>**Input:** Due sequenze di bit (A e B)
>
>**Output:** Z (bit singolo)
>
>$$
>Z= \begin{cases}
>0 &\text{if }\ A \not= B \\
>1 &\text{if }\ A = B \\
>\end{cases} \\
>$$

---
## Circuito interno

Il comparatore logico confronta sequenze di `n` bit, *utilizzando porte [[Operatori Booleani e Porte Logiche#XOR|XOR]] per comparare ogni coppia di bit*, gli output delle [[Operatori Booleani e Porte Logiche#XOR|XOR]] confluiscono in una [[Operatori Booleani e Porte Logiche#NOR|NOR]], che restituisce 1 se le sequenze sono uguali e 0 se sono diverse.

>[!note] Circuito
>![[Pasted image 20240203120009.png|400]]
>
>>**OSS:** Basta una xor con output 1 per far uscire la somma tra tutte le xor 1, che una volta negata viene 0

>[!warning] Nota (funzionamento XOR)
> [[Operatori Booleani e Porte Logiche#XOR|XOR]] restituisce: 
>- 0 quando due bit sono **uguali** 
>- 1 quando sono **diversi**
