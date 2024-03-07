---
Created: 2023-03-30
Type: Programming Note
Programming Language: "[[C MOC]]"
Related:
  - "[[C Pointers]]"
Completed: true
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
