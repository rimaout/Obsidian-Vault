---
Created: 2024-03-05
Type: Uni Note
Class:
  - "[[Architettura (class)]]"
Academic Year: 2023/2024
Related: 
Completed: false
---
---

>[!info] Index
>1. 

---

[[CISC (Complex Instruction Set Computer)]]
[[RISC (Reduced Instruction Set Computer)]]

## Differenze


>[!info] CISC
>**Istruzioni di dimensione variabile:**
>- Per il fetch della successiva è necessaria la decodifica della prededente
>
>**Formato variabile:**
>- Decodifica complessa
>
>**Operandi in memoria:**
>- Molti accessi alla memoria per istruzione
>
>**Pochi registri interni:**
>- Maggior numero di accessi in memoria
>
>**Modi di indirizzamento complessi:**
>- Maggior numero di accessi in memoria
>- Durata variabile della istruzione
>- Conflitti tra istruzioni più complicati
>
>**Istruzioni Complesse:** 
>- Pipeline più complicata
>- Più veloci a nello svolgere operazioni complesse


>[!info] RISC
>**Istruzioni di dimensione fissa:**
>- Fetch della successiva senza decodifica della precedente
>
>**Istruzioni di formato uniforme:**
>- Per semplificare la fase di decodifica
>
>**Operazioni ALU solo tra registri:**
>- Senza accesso a memoria
>
>**Molti registri interni:**
>- Per i risultati parziali senza accessi alla memoria
>
>**Modi di indirizzamento semplici:**
>- Con spiazzamento, 1 solo accesso a memoria
>- Durata fissa della istruzione
>- Conflitti semplici
>
>**Istruzioni Semplici:** 
>- Pipeline più veloce
>- Più lento nello svolgere operazioni complesse

---