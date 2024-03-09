---
Created: 2024-03-08
Type: Uni Note
Class:
  - "[[Architettura (class)]]"
Academic Year: 2023/2024
Related:
  - "[[MIPS]]"
Completed: false
---
---

>[!info] Index
>1. [[#Aritmetiche]]
>2. [[#Trasferimento di dati]]
>3. [[#Logiche]]
>4. [[#Salti condizionali]]
>5. [[#Salti incondizionati]]

---

### Aritmetiche

| Istruzioni      | Esempio           | Significato       | Commenti                              |
| --------------- | ----------------- | ----------------- | ------------------------------------- |
| Somma           | `add $s1,$s2,$s3` | `$s1 = $s2 + $s3` | Operandi in tre registri              |
| Sottrazione     | `sub $s1,$s2,$s3` | `$s1 = $s2 - $s3` | Operandi in tre registri              |
| Somma immediata | `addi $s1,$s2,20` | `$s1 = $s2 + 20`  | Utilizzata per sommare delle costanti |

---
### Trasferimento di dati

| Istruzioni                                        | Esempio           | Significato                               | Commenti                                                                |
| ------------------------------------------------- | ----------------- | ----------------------------------------- | ----------------------------------------------------------------------- |
| Lettura parola                                    | `lw $s1,20($s2)`  | `$s1 = Memoria[$s2+20]`                   | Trasferimento di una parola da memoria a registro                       |
| Memorizzazione parola                             | `sw $s1,20($s2)`  | `Memoria[$s2+20]=$s1`                     | Trasferimento di una parola da registro a memoria                       |
| Lettura mezza parola                              | `lh $s1,20($s2)`  | `$s1=Memoria[$s2+20]`                     | Trasferimento di una mezza parola da memoria a registro                 |
| Lettura mezza parola senza segno                  | `lhu $s1,20($s2)` | `$s1=Memoria[$s2+20]`                     | Trasferimento di una mezza parola da memoria a registro                 |
| Memorizzazione mezza paola                        | `sh $s1,20($s2)`  | `Memoria[$s2+20]=$s1`                     | Trasferimento di una mezza parola da memoria a registro                 |
| Lettura byte                                      | `lb $s1,20($s2)`  | `$s1=Memoria[$s2+20]`                     | Trasferimento di un byte da memoria a registro                          |
| Lettura byte senza segno                          | `lbu $s1,20($s2)` | `$s1=Memoria[$s2+20]`                     | Trasferimento di un byte da memoria a registro                          |
| Memorizzazione byte                               | `sb $s1,20($s2)`  | `Memoria[$s2+20]=$s1`                     | Trasferimento di un byte da registro a memoria                          |
| Lettura di una parola e blocco                    | `ll $s1,20($s2)`  | `$s1=Memoria[$s2+20]`                     | Caricamento di una parola come prima fase di un’operazione atomica      |
| Memorizzazione condizionata di una parola         | `sc $s1,20($s2)`  | `Memoria[$s2+20]=$s1`<br>`$s1=0` oppure 1 | Memorizzazione di una parola come seconda fase di un’operazione atomica |
| Caricamento costante nella mezza parola superiore | `lui $s1,20`      | `$s1 = 20 * 2^16`                         | Caricamento di una costante nei 16 bit più significativi                |

---
### Logiche

| Istruzioni                    | Esempio           | Significato           | Commenti                                                            |
| ----------------------------- | ----------------- | --------------------- | ------------------------------------------------------------------- |
| And                           | `and $s1,$s2,$s3` | `$s1 = $s2 & $s3`     | Operandi in tre registri; AND bit a bit                             |
| Or                            | `or $s1,$s2,$s3`  | `$s1 = $s2 \| $s3`    | Operandi in tre registri; OR bit a bit                              |
| Nor                           | `nor $s1,$s2,$s3` | `$s1 = ~($s2 \| $s3)` | Operandi in tre registri; NOR bit a bit                             |
| And immediato                 | `andi $s1,$s2,20` | `$s1 = $s2 & 20`      | AND bit a bit tra un operando in registro e una costante            |
| Or immediato                  | `ori $s1,$s2,20`  | `$s1 = $s2 \| 20`     | OR bit a bit tra un operando in registro e una costante             |
| Scorrimento logico a sinistra | `sll $s1,$s2,10`  | `$s1 = $s2 << 10`     | Spostamento a sinistra del numero di bit specificato della costante |
| Scorrimento logico a destra   | `srl $s1,$s2,10`  | `$s1 = $s2 >> 10`     | Spostamento a destra del numero di bit specificato di una costante  |

---
### Salti condizionali


---
### Salti incondizionati 


---