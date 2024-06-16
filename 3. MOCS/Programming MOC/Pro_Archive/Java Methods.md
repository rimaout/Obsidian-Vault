---
created: 2024-03-08
type: Programming Note
programming language: "[[Java MOC]]"
related:
  - "[[Java OOP]]"
completed: false
updated: 2024-06-16T17:44
---
---

>[!info] Index
>1. [[#Metodi]]
>2. [[#Declaring a Java Method]]

---
## Metodi 


---
## Declaring a Java Method

The syntax to declare a method is:

```java
modifier static returnType nameOfMethod (type parameter1, type parameter2, ...) {
  // method body
}
```

>[!tip]
>- `returnType` - It specifies what type of value a method returns For example if a method has an `int` return type then it returns an integer value.        
>- `methodName` - It is an [identifier](https://www.programiz.com/java-programming/keywords-identifiers#identifiers) that is used to refer to the particular method in a program
>- `modifier` - It defines access types whether the method is public, private, and so on. To learn more, visit [[Java Access Modifiers]]
>- `parameter1/parameter2` - These are values passed to a method. We can pass any number of arguments to a method.
>- `static` - If we use the `static` keyword, it can be accessed without creating objects.  
>	- For example, the `sqrt()` method of standard [[Java Math class]] is static. Hence, we can directly call `Math.sqrt()` without creating an instance of `Math` class.

>[!warning] oss
>- If the method does not return a value, its **returnType** is `void`.
>- il `modifier` di metodo è tipicamente pubblico, ovvero visibile a tutti

---
