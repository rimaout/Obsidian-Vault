---
Created: 2024-03-16
Type: Uni Note
Class:
  - "[[Architettura (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Architettura MIPS]]"
Completed: true
---
---

>[!info] Index
>1. [[#Introduzione]]
>2. [[#Microprocessori]]
>3. [[#Registri]]

---
## Introduzione

In particolare, l’Architettura MIPS 2000 è composta da:
- Tutte le word hanno una dimensione fissa di 32 bit
- Lo spazio di indirizzamento è di 230 word di 32 bit ciascuna, per un totale di 4 GB
- Una memoria indicizzata al byte, dunque, dato un indirizzo di memoria t corrispondente all’inizio di una word, per leggere la word successiva è necessario utilizzare l’indirizzo t + 4, poiché 4 byte corrispondono a 32 bit (ricordiamo che ogni word è composta da 32 bit)
- Gli interi vengono salvati utilizzando la notazione del Complemento a 2 su 32 bit

---
## Microprocessori

L'[[Architettura MIPS]] dotata di 3 microprocessori:
- La CPU principale, dotata di ALU, di 32 registri HI/LO ed addetta all’esecuzione delle istruzioni
-  Il Coprocessore 0, non è dotato di registri e non ha accesso alla memoria, ma è solo addetto alla gestione di "trap", eccezioni, Virtual Memory, Cause, EPC, Status, BadVAddr, ...	
-  Il Coprocessore 1, addetto ai calcoli in virgola mobile e dotato di 32 registri da 32 bit, utilizzabili anche come 64 registri da 16 bit

---
## Registri

![[Registri MIPS]]

---