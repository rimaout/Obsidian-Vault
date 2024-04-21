---
Created: 2024-03-13
Type: Programming Note
Programming Language: "[[Java MOC]]"
Related: 
Completed: true
---
---

>[!info] Index
>1. [[#Java if Statement]]
>2. [[#Java if...else Statement]]
>3. [[#Java if...else...if Statement]]
>4. [[#Java short hand `if...else` statement]]

---
## Java if Statement

The syntax of an **if-then** statement is:

```java
if (condition) {
  // statements
}
```

Here, condition is a boolean expression such as `age >= 18`.

- if condition evaluates to `true`, statements are executed
- if condition evaluates to `false`, statements are skipped

---
## Java if...else Statement
Statements inside the body of `else` block are executed if the test expression is evaluated to `false`. 

```java
if (condition) {
  // codes in if block
}
else {
  // codes in else block
}
```

---
## Java if...else...if Statement
**if...else...if** can be used to execute one block of code among multiple other blocks.

```java
if (condition1) {
  // codes
}
else if(condition2) {
  // codes
}
else if (condition3) {
  // codes
}
.
.
else {
  // codes
}
```

Here, `if` statements are executed from the top towards the bottom. When the test condition is `true`, codes inside the body of that `if` block is executed. And, program control jumps outside the **if...else...if** ladder.

If all test expressions are `false`, codes inside the body of `else` are executed.

---
## Java short hand `if...else` statement
There is also a short-hand if else, which is known as the **ternary operator** because it consists of three operands.

It can be used to replace multiple lines of code with a single line, and is most often used to replace simple if else statements:

**Syntax:**
```java
variable = (condition) ? expressionTrue :  expressionFalse;
```

---