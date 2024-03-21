---
Created: 2024-03-08
Type: Uni Note
Class:
  - "[[Architettura (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Architettura MIPS]]"
Completed: false
---
---

>[!info] Index
>1. 

---
## Rappresentazione dell'istruzione
Assemblatole converte un istruzione (esempio: `add $t0, $s1, $s2`) in una sequenza di 32 bit

Esistono 2 tipo
- [[#R-type]]
- [[#I-type]]

### R-type
![[Pasted image 20240308112921.png|500]]

### I-type

tipo immediato 

![[Pasted image 20240308113041.png|500]]

possono essere usate anche per i salti inseriamo nella parte immediata ...

---
### J-type

- salti non condizionati (salto assoluto)

i 26 bit restanti vengono utilizzati per il salto (in realtà ne servono 32)
