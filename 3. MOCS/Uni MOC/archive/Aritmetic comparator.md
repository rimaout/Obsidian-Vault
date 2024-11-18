---
created: 2024-02-03
type: Uni Note
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
academic year: 2023/2024
related:
  - "[[Uni MOC]]"
completed: true
updated: 2024-11-18T20:21
---
>[!abstract] Index
>1. [[#Introduzione]]
>2. [[#Implementazione]]

>[!abstract] Related
>- [[Circuiti combinatori]]
>- [[Circuiti combinatori]]
>- [[Progettazione Sistemi Digitali (class)]]

---
## Introduzione

**Comparatore Aritmetico** confronta la *magnitudo*[^1] tra due 

>[!note] Rappresentazione circuitale
>![[Pasted image 20240203131233.png|200]]

>[!warning] Input / Output
>**Input:** Due numeri A e B
>
>**Output:**
>- `A = B`
>- `A > B`
>- `A < B`
>
>>**Nota:** 
>>- Gli Input `A` e `B` sono sequenze di bit
>>- Gli Output `=`, `>`, `<` sono singoli bit che assumono i vali 1 (True) e 0 (False) 

---
## Implementazione 

>[!note] A = B 
>Si utilizza un [[Logic comparator|comparatore logico]].

>[!note] A > B 
>Si utilizza: 
>1. Un [[Circuiti Aritmetici|adder]] per effettuare $A-B$, 
>2. Poi si usa un circuito che ha come output:
>	- 1 se il *MSB*[^2] dell' risultato dell'operazione è uguale a 0.
>	- 0 se il *MSB*[^2] dell' risultato dell'operazione è uguale a 1.

>[!note] A < B 
>Si utilizza un [[Operatori Booleani e Porte Logiche#AND|and]] con input *A = B* e *A > B* negati, se gli input sono tutti e due uguali zero allora l'output della and sarà uno.

---

[^1]: Magnitudo: Grandezza di un numero, due numeri che hanno la stessa magnitudo sono uguali, un numero x che ha una magnitudo superiore rispetto a un numero y significa che x > y.

[^2]: MSB: Most significant bit, quando si parla di numeri binari è il bit più a sinistra.