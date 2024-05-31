---
created: 2024-04-07
type: Programming Note
programming language: "[[MIPS Assembly MOC]]"
related: 
completed: false
updated: 2024-05-27T13:29
---
---

>[!abstract] Index
>1. [[#Main Directives]]
>2. [[#.data directives]]

>[!abstract] Related
>1. [[Architettura dei calcolatori (class)]]
>2. [[MIPS Assembly MOC]]

---
## Main Directives

| Syntax  | Meaning                                                                                                                       |
| ------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `.main` | It's used to mark a file as the main file (the one that is run first)                                                         |
| `.data` | Introduces the data (i.e. global variables) section of the program, this variables are stored in the computer memory (RAM ??) |
| `.text` | Introduces the text (i.e. code) section of the program.                                                                       |

## .data directives

Directives which can only be used in a `.data` section of the program file:

| Syntax                 | Meaning                                                                          | Example               |
| :--------------------- | :------------------------------------------------------------------------------- | :-------------------- |
| `.asciiz <characters>` | _characters_ will be stored in memory as a zero byte terminated string constant. | .asciiz "Hello world" |
| `.space <number>`      | _number_ of bytes is reserved in memory.                                         | .space 400            |
| `.word <number>`       | The 32-bit number _number_ is stored in memory.                                  | .word 1234            |

>[!tip]- Example
>```javascript
>.data
>	string: .asciiz "ciao mondo"
>	number: .word 1  // number = 0000000000000000000000000000001
>	
>```

---
