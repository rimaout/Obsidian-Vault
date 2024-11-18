---
created: 2023-03-30
type: Programming Note
programming language: "[[C MOC]]"
related:
  - "[[C Pointers]]"
completed: true
updated: 2024-05-27T13:29
---
---
- When a variable is created in C, a memory address is assigned to the variable.
	- The memory address is the location of where the variable is stored on the computer.
- When we assign a value to the variable, it is stored in this memory address.

---
## How to access the memory address of a variable
To access it, use the reference operator (`&`), and the result represents where the variable is stored:

#### Example:
```c
int myAge = 43;  
printf("%p", &myAge); // Outputs 0x7ffe5367e044
```

>[!warning] Note:
>The memory address is in ***hexadecimal*** form (0x..)

>[!warning] Note:
>You should also note that `myAge` is often called a "pointer". A pointer basically stores the memory address of a variable as its value. To print pointer values, we use the `%p` format specifier.

**Learn more about pointers:** [[C Pointers]]
