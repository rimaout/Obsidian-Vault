---
Created: ""
Type: Programming Note
Programming Language: 
Related: 
Completed: false
---
---

>[!abstract] Index
>1. 

>[!abstract] Related
>1. [[MIPS Assembly MOC]]
>2. [[Architettura dei calcolatori (class)]]

---
## Addition

>[!note] Syntax
>```javascript
>add  $t1, $t2, t3      # set $t1 to $t2 + $t3
>addi $t1, $t2, imm     # set $t1 to $t2 + imm
>```
>**oss:** `imm` is a `halfword` (16 bit)

>[!tip] Example
>```javascript
>add  $t3, $t1, $zero     # t3 = t1 + 0
>addi $t1, $t0, 100       # t1 =  0 + 100
>```

---
## Subtraction

>[!note] Syntax
>```javascript
>sub  $t1, $t2, t3      # set $t1 to $t2 - $t3
>subi $t1, $t2, imm     # set $t1 to $t2 - imm
>```
>**oss:** `imm` is a `halfword` (16 bit)

>[!tip] Example
>```javascript
>sub  $t3, $t1, $zero     # t3 = t1 - 0
>subi $t1, $t0, 100       # t1 =  0 - 100
>```
