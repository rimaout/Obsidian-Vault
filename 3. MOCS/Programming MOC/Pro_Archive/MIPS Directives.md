---
Created: 2024-04-07
Type: Programming Note
Programming Language: "[[MIPS Assembly MOC]]"
Related: 
Completed: false
---
---

>[!info] Index
>1. 

---

| Syntax  | Meaning                                                             |
| ------- | ------------------------------------------------------------------- |
| `.data` | Introduces the data (i.e. global variables) section of the program. |
| `.text` | Introduces the text (i.e. code) section of the program.             |

**Directives which can only be used in a .data section of an assembly language program file:**

| Syntax                 | Meaning                                                                          | Example               |
| :--------------------- | :------------------------------------------------------------------------------- | :-------------------- |
| `.asciiz <characters>` | _characters_ will be stored in memory as a zero byte terminated string constant. | .asciiz "Hello world" |
| `.space <number>`      | _number_ of bytes is reserved in memory.                                         | .space 400            |
| `.word <number>`       | The 32-bit number _number_ is stored in memory.                                  | .word 1234            |
