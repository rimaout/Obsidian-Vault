---
created: 2024-03-07
type: Programming Note
programming language: "[[Java MOC]]"
related:
  - "[[Java built-in data types]]"
completed: false
updated: 2024-05-27T13:29
---
---
>[!abstract] Page Index
>1. [[#Introduction]]
>2. [[#How to create a string]]
>3. [[#f string]]

>[!abstract] Related
>- [[Java Strings Methods]]
>- [[Java String Builder]]

---
## Introduction

In Java, a `String` is a class, not a primitive data type. It represents a sequence of characters. 

Unlike primitive data types, a `String` is an object, which means it has [[Java Strings Methods|methods]] you can use, support for character strings is implemented via `java.lang.String class`.

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
## f string

Java you can use `String.format()` method which works similarly to [[Java Output#printf()|`printf()`]]. It allows you to create a new string using a format string and arguments. Here is an example:

```java
String name = "John";
int age = 30;

String formattedString = String.format("Hello, my name is %s and I am %d years old.", name, age);
System.out.println(formattedString);
```


In this example, `%s` is a placeholder for a string, and `%d` is a placeholder for an integer. The variables `name` and `age` are inserted into these placeholders respectively.

---
