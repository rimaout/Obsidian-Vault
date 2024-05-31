---
created: 2023-03-20
type: Programming Note
programming language: "[[C MOC]]"
related: 
completed: true
updated: 2024-05-27T13:29
---
---
## Single-line Comments

Single-line comments start with two forward slashes (`//`).

Any text between `//` and the end of the line is ignored by the compiler (will not be executed).
```C
// This is a comment  
printf("Hello World!");

printf("Hello World!"); // This is a comment
```
---

## C Multi-line Comments

Multi-line comments start with `/*` and ends with `*/`.

Any text between `/*` and `*/` will be ignored by the compiler:
```C
/* The code below will print the words Hello World!  
to the screen, and it is amazing */  
printf("Hello World!");
```

---
