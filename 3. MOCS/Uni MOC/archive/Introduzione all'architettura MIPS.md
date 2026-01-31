---
created: 2024-03-16
type: Uni Note
class:
  - "[[Architettura dei calcolatori (class)]]"
academic year: 2023/2024
related:
  - "[[Architettura MIPS]]"
completed: true
updated: 2026-01-31T13:32
---
---

>[!info] Index
>1. [[#Introduzione]]
>2. [[#Microprocessori]]
>3. [[#Registri]]

>[!note] Related
>- [[Architettura dei calcolatori (class)]]
>- [[Architettura MIPS]]

---
## Introduzione

>[!note] Caratteristiche Architettura MIPS 2000 
>- **Word** dimensione di ==32 bit==
>- Lo **spazio di indirizzamento **è di 230 word di 32 bit ciascuna, per un totale di ==4 GB==
>- Gli **interi** sono rappresentati in [[Codifica complemento a due (CA2)]] a 32 bit
>- Una **memoria indicizzata** al ==byte==, dunque, 
>	- *oss:* dato un indirizzo di memoria t corrispondente all’inizio di una word, per leggere la word successiva è necessario utilizzare l’indirizzo t + 4, poiché 4 byte corrispondono a 32 bit (ricordiamo che ogni word è composta da 32 bit)

---
## Microprocessori

L'Architettura MIPS dotata di 3 microprocessori:
- **[[ALU (Arithmetic Logic Unit)]]** di 32 registri HI/LO ed addetta all’esecuzione delle istruzioni
-  Il **Coprocessore 0** è solo addetto alla gestione di "trap", eccezioni, Virtual Memory, Cause, EPC, Status, BadVAddr, ...	
-  Il **Coprocessore 1**, addetto ai calcoli in virgola mobile e dotato di 32 registri da 32 bit, utilizzabili anche come 64 registri da 16 bit

---
## Registri

![[Registri MIPS]]

---