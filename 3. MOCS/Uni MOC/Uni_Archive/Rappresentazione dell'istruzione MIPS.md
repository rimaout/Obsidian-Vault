---
created: 2024-03-08
type: Uni Note
class:
  - "[[Architettura dei calcolatori (class)]]"
academic year: 2023/2024
related:
  - "[[Architettura MIPS]]"
completed: false
updated: 2024-05-27T13:29
---
---

>[!abstract] Index
>1. [[#Introduzione]]
>2. [[#R-type]]
>3. [[#I-type]]
>4. [[#J-type]]

>[!abstract] Related
>- [[MIPS Assembly MOC|MIPS Assembly]]
>- [[Architettura dei calcolatori (class)]]

---
## Introduzione
Ogni Istruzione è rappresentata in 32 bit, assegnando significati diversi a sequenze di questi bit sono state decise 3 principali formattazioni per le istruzioni:
1. [[#R-type]]
2. [[#I-type]]
3. [[#J-type]]

>[!note] Formattazione delle istruzioni:
>![[Pasted image 20240416154612.png|700]]
>- `31 26 - 25 21 - ... - 05 00`  sono i range di bit in cui sono rappresentati i parametri delle istruzioni ad esempio, in J-Type dal bit 31 al 26 è contenuta l'opcode e dal 25 allo 0 l'indirizzo.

>[!tip] Significato acronimi
>- `opcode:` operation code
>- `rs:` first register source operand
>- `rt:` second register source operand
>- `rd:` register destination operand 
>- `shamt:` shift amount
>- `funct:` function code

---
## R-type

Le istruzioni R-type eseguono **operazioni aritmetico/logiche**.

| `op`  | `rs`  | `rt`  | `rd`  | `shamt` | `funct` |
| ----- | ----- | ----- | ----- | ------- | ------- |
| 6 bit | 5 bit | 5 bit | 5 bit | 5 bit   | 6 bit   |

I 32 bit sono suddivisi in:
- `opcode:`operazione base dell’istruzione
- `rs:` registro contenente il primo operando sorgente
- `rt:` registro contenente il secondo operando sorgente
- `rd:` registro di destinazione
- `shamt:` numero di posizioni di scorrimento (utilizzato solo per operazioni di shifting, default zero)
- `funct:` specifica la variante dell’operazione base definita dal codice operativo

>[!tip]- Esempio
>Quindi se faccio `add $t0,$s1,$s2`
>
>| `op`  | `rs`  | `rt`  | `rd`  | `shamt` | `funct` |
>| ----- | ----- | ----- | ----- | ------- | ------- |
>| 000000 | 10001 | 10010 | 01000 | 00000 | 100000 |
>| 6 bit | 5 bit | 5 bit | 5 bit | 5 bit   | 6 bit   |
>
>`rd` corrisponderà a t0
>`rs` corrisponderà a s1
>`rt` corrisponderà a s2

---
## I-type

Le istruzioni di tipo **I-type** (immediato), hanno 16 bit per un indirizzo di memoria (o meglio una sua parte) o una costante.

| `op`  | `rs`  | `rt`  | `imm`  |
| ----- | ----- | ----- | ------ |
| 6 bit | 5 bit | 5 bit | 16 bit |

I 32 bit sono suddivisi in:
- `opcode:`operazione base dell’istruzione
- `rs:` registro contenente il primo operando sorgente
- `rt:` registro contenente il secondo operando sorgente
- `imm:` costante o indirizzo

>[!note] Utilizzo
>Questo tipo di istruzione è utilizzato per effettuare operazioni di tipo:
>- `load`/`store` dove `imm` (ultimi 16 bit) è utilizzata per passare una costante
>- `salti` di tipo immediato dove `imm` (ultimi 16 bit) è utilizzata per passare una indirizzo di un indirizzo del pc

>[!tip]- Esempio
>Quindi se faccio `addi $t2,$s2,4`
>
>| `op`  | `rs`  | `rt` | `imm` |
>| ----- | ----- | ----- | ----- | ------- | ------- |
>| 00 1000 | 0 1010 | 0 1010 | 0000 0000 0000 0100 |
>| 6 bit | 5 bit | 5 bit | 16 bit  |

---
## J-type

Le istruzioni di tipo **J-type** permettono di effettuare salti non condizionati (salti assoluti).

| `op`  | `address` |
| ----- | --------- |
| 6 bit | 26 bit    |

I 32 bit sono suddivisi in:
- `opcode:`operazione base dell’istruzione
- `address:` registro contenente il primo operando sorgente

>[!tip]- Esempio
>Quindi se faccio `addi $t2,$s2,4`
>
>| `op`  | `rs`  | `rt` | `imm` |
>| ----- | ----- | ----- | ----- | ------- | ------- |
>| 00 1000 | 0 1010 | 0 1010 | 0000 0000 0000 0100 |
>| 6 bit | 5 bit | 5 bit | 16 bit  |

---