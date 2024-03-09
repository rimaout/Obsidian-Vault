---
Created: 2024-03-07
Type: Programming Note
Programming Language: "[[Java MOC]]"
Related:
  - "[[Java built-in data types]]"
Completed: false
---
---
## Java Strings
In Java, a `String` is a class, not a primitive data type. It represents a sequence of characters. 

Unlike primitive data types, a `String` is an object, which means it has [[Java Strings Methods|methods]] you can use, support for character strings is implemented via `java.lang.String class`.

>[!info] Index
>- [[Java Strings Methods]]
>- [[#How to create a string]]

---
## How to create a string

In Java, `String` is a special class and you can initialise a `String` object using string literals directly, without the need to call a constructor. 

 Here's an example of creating a `String` using a constructor:
```java
char[] charArray = {'H', 'e', 'l', 'l', 'o'};
String str = new String(charArray);
System.out.println(str);  // Outputs: Hello
```

However, it's important to note that it's more common and simpler to create a `String` object directly from a string literal, like this:

```java
String str = "Hello";
System.out.println(str);  // Outputs: Hello 
```

---
