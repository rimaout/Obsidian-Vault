---
Created: 2024-03-12
Type: Programming Note
Programming Language: "[[Java MOC]]"
Related:
  - "[[Java Create a Package]]"
Completed: true
---
---

>[!info] Index
>1. [[#How import works?]]
>2. [[#Importing a class]]
>3. [[#Importing a Package]]

---
## How import works?

Java has an `import` statement that allows you to:
```java
import package.name.ClassName;   // To import a certain class only
import package.name.*   // To import the whole package
```

---
## Importing a class
- Utilizzata per non dichiarare il package ogni volta che si vuole utilizzare una determinata classe

```java
import java.util.Scanner;

// posso scrivere
Scanner input = new Scanner(System.in);

// invece di
java.util.Scanner input = new java.util.Scanner(System.in)
```

---
## Importing a Package
- L’intero package:

```java
import java.util. \*;
```

>[!warning] \* non è ricorsivo
>Quindi i sub package contenuti dal main package non sono inportati

---