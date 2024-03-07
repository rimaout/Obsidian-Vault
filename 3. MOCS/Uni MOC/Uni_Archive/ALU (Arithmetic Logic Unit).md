---
Created: 2024-02-03
Type: Uni Note
Class:
  - "[[Progettazione Sistemi Digitali (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Circuiti combinatori]]"
  - "[[Circuiti Aritmetici]]"
Completed: false
---
---
## Index
1. [[#Definizione]]

---
## Definizione 
ALU è un [[Circuiti combinatori|circuito combinatorio]] che svolge:
- Operazioni logiche (su singoli bit o bitwise) come l'[[Operatori Booleani e Porte Logiche#AND|and]] o l'[[Operatori Booleani e Porte Logiche#OR|or]].
- Operazioni aritmetiche di base, somma, sottrazioni, moltiplicazione e divisione.

>[!warning] Rappresentazione circuitale
![[Pasted image 20240204194514.png|300]]

>[!danger] I/O
>**Input:**
>- *A* e *B* sono sequenze di bit
>
> **Output:**
> - *R* risultato dell'operazione
> - Le *ALU* sono dotate anche di 4 output aggiuntivi, i bit del *condition code* (bit di controllo):
> 	- ﻿﻿W - overflow
> 	- ﻿﻿N- risultato negativo
> 	- ﻿﻿Z - risultato pari a 0
> 	- ﻿﻿C - riporto in uscita

---