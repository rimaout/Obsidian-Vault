---
created: 2024-04-08
type: Programming Note
programming language: "[[Java MOC]]"
related: 
completed: true
updated: 2024-05-27T13:29
---
---

>[!info] Index
>1. [[#Java switch Statement]]
>2. [[#Example + Compact version]]
>3. [[#Java yield]]

---
## Java switch Statement

Instead of writing **many** `if..else` statements, you can use the `switch` statement.

The `switch` statement selects one of many code blocks to be executed:


**Syntax:**
```java
switch(expression) {
  case x:
    // code block
    break;
  case y:
    // code block
    break;
  default:
    // code block
}
```

>[!warning] oss
>The default value catch all the not specified cases

---
## Example + Compact version

![[Pasted image 20240312112641.png|800]]

---
## Java yield

- The keyword “yield” in Java is used in switch expressions to provide a returned value
- The “yield” keyword allows you to exit a switch expression by returning a value, which becomes the value of the switch expression.

**Example:**
```java
String number = switch (number) {
    case 1:
        yield "one";
    case 2:
        yield "two";
    default:
        yield "Zero";
}
```

---