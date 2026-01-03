---
created: 2024-02-28
type: Programming Note
programming language: "[[Java MOC]]"
related:
  - "[[Java Literals]]"
completed: true
updated: 2025-01-25T19:16
---
---

>[!info] Index
>1. [[#Java Variables]]
>2. [[#Create Variables in Java]]
>3. [[#Change values of variables]]
>4. [[#Unmutable Variables]]
>5. [[#Rules for Naming Variables in Java]]
>6. [[#Naming conventions]]

---
## Java Variables

>[!def] Definition
>A variable is a location in memory (storage area) to hold data.

To indicate the storage area, each variable should be given a unique name (identifier). 

>[!info]
There are 4 types of variables in Java programming language:
>- Instance Variables (Non-Static Fields)
>- Class Variables (Static Fields)
>- Local Variables
>- Parameters
>
>If you are interested to learn more about it now, visit [Java Variable Types](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/variables.html).

---
### Create Variables in Java

Here's how we create a variable in Java:

```
type variable
```

```java
int speedLimit = 80;
```

The int data type suggests that the variable can only hold integers. To learn more, visit [[Java built-in data types]]

You can also declare variables and assign variables separately:

```java
int speedLimit;
speedLimit = 80;
```

>[!Note] 
>Java is a **statically-typed language**. It means that all variables must be declared before they can be used.

---
### Change values of variables

The value of a variable can be changed in the program. For example,

```java
int speedLimit = 80;
...
speedLimit = 90;
```

However, we cannot change the data type of a variable in Java within the same scope:

```java
int speedLimit = 80;
...
float speedLimit;
```

```
Error: variable s is already defined in method ...
```

---
### Unmutable Variables

```java
final String name = "rimaout"
```

---
### Rules  for Naming Variables in Java

Java programming language has its own set of rules and conventions for naming variables. Here's what you need to know:

- Java is **case sensitive**. Hence, age and AGE are two different variables. For example,  
     
- Variables must start with either a **letter** or an **underscore**, **\_** or a **$**.
    ```java
    int age;   // valid name and good practice
    int _age;  // valid but bad practice
    int $age;  // valid but bad practice
    ```
    
- Variable names cannot start with numbers.
    ```java
    int 1age;  // invalid variables
    ```
    
- Variable names can't use white space. 
    ```java
    int my age;  // invalid variables
    ```
    
###### Naming conventions

![[signal-2024-03-03-130943_002.png|600]]

If you choose **one-word variable names**, use all lowercase letters. 
```java
int speed    // good practise

int SPEED    // bad practise
int Speed    // bad practise
```

Java uses the **Camel case notation**, if we need to use variable names having more than one word, use all lowercase letters for the first word and capitalise the first letter of each subsequent word.  

```
Examples: myAge, speedLimit
```