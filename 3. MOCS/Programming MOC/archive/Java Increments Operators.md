---
created: 2024-03-07
type: Programming Note
programming language: "[[Java MOC]]"
related:
  - "[[Java Operators]]"
completed: true
updated: 2024-05-27T13:29
---
---
## Increments Operators

- Post-increment:
    - `var++` (var = var +1)
    - `var--`
- Pre-increment:
    - `++var`
    - `--var`

**Pre vs Post-increment:** 
- In an expression, the post-increment `a++` first performs the operation with `a`, and then increments it by 1. Therefore:
```java
	 

int a = 3;

int c = a++ // c == 3, a == 4

int a = 3;

int c = ++a // c == 4, a == 4

int a = 4;

int c = 3;

int z = (a++) - (c--); // z == 1, a == 5, c == 2
```

In the first example, `c` is assigned the current value of `a`, then `a` is incremented. In the second example, `a` is incremented first, then its value is assigned to `c`. In the third example, `a` is incremented and `c` is decremented after the subtraction operation.

---

