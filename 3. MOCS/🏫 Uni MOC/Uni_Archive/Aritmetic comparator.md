---
Created: 2024-02-03
Type: Uni Note
Class:
  - "[[Progettazione Sistemi Digitali (class)]]"
Academic Year: 2023/2024
Related:
  - "[[🏫 Uni MOC]]"
Completed: true
---
---
## Index

1. [[#Definizione]]
2. [[#Calcolo numero variabili]]
3. [[#Circuito interno]]

---
## Definizione

**Comparatore Aritmetico** confronta la *magnitudo*[^1] tra due 

>[!warning] Rappresentazione circuitale
>![[Pasted image 20240203131233.png|200]]

**Input:** Due numeri A e B (espressi come sequenze di bit)

**Output:**
- $A = B$
- $A>B$
- $A<B$    (se entrambi > e = sono FALSE)

---
## Funzionamento 

 Per controllare se:
- **A = B** -> si utilizza un [[Logic comparator|comparatore logico]].
- **A > B** -> si utilizza un [[Circuiti Aritmetici|adder]] per effettuare $A-B$, poi si usa un circuito che da come output 1 se il *MSB*[^2] dell' risultato dell'operazione è uguale a 0.
- **A < B** -> si utilizza un [[Operatori Booleani e Porte Logiche#AND|and]] con input *A = B* e *A > B* negati, se gli input sono tutti e due uguali zero allora l'output della and sarà uno.

[^1]: Magnitudo: Grandezza di un numero, due numeri che hanno la stessa magnitudo sono uguali, un numero x che ha una magnitudo superiore rispetto a un numero y significa che x > y.

[^2]: MSB: Most significant bit, quando si parla di numeri binari è il bit più a sinistra.