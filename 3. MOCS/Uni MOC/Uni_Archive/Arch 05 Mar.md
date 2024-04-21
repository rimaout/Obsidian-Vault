---
Created: 2024-03-05
Type: Uni Note
Class:
  - "[[Architettura dei calcolatori (class)]]"
Academic Year: 2023/2024
Related: 
Completed: false
---
---

>[!info] Index
>1. 

---
### CPU
![[Pasted image 20240305121228.png|300]]

**Alu:**
- fa solo calcoli 
- non ha uno stato interno

**Registri:**
- a uso generale e speciale
- manipolazione di istruzioni, indirizzi, dati, risultati

**Bus:**
- bus di comunicazione con la memoria 
- bus di comunicazione con periferiche (non necessario con memory mapping)

**CU:** 
- Unità di controllo (instuction decoder nella figura)

---

>[!note] Nibble
un nibble è una sequenza di 4 bit

---

## Architettura CISC e RISC

`CISC:` Complex Instruction Set Computer
`RISC:` Reduced Instruction Set Computer

>[!note] CISC
>- **Istruzioni di dimensione variabile**
>	- per il fetch della successiva è necessaria la decodifica 
>- **Formato variabile**
>	- decodifica complessa
>- **Operazioni in memoria**
>	- molti accessi alla memoria per istruzione 
>- **Pochi registri interni:**
>	- magior numero di 

da continuaere

>[!note] RISC
>


---
## MIPS


### Memoria
- memoria descritta in byte
- composta da 32 registri (architettura a 32 bit)
- se sono all'indirizzo `t` e voglio leggere la parola successiva incremento `t+4`, questo perché una parola sono 4 byte ovvero 32 bit

## Linguaggio Assembly MIPS

**Rappresentazione dell’istruzione (R-type):**

![[Pasted image 20240305134628.png|800]]

`op` operation code
`rs` first register source operand
`rt` second register source operand 
`rd` register destination operand 
`shamt` shift amount 
`funct` function (code)

---
