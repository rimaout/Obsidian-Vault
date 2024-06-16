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
>1. [[#Introduzione]]
>2. [[#Class Structure]]
>3. [[#Create a class in Java]]

---
## Introduzione
Java is an object-oriented programming language. The core concept of the object-oriented approach is to break complex problems into smaller objects.

An object is any entity that has a **state** and **behaviour**. For example, a bicycle is an object. It has:
- **States** (fields): idle, first gear, etc
- **Behaviours** (methods): braking, accelerating, etc.

Before we learn about objects, let's first know about classes in Java

Una classe è un pezzo di codice all'interno di un programma che descrive un particolare tipo di oggetti 

La classe fornisce un prototipo astratto gli oggetti di un particolare tipo, definendo la loro struttura in termini di:
-  Campi (stato) degli oggetti
-  Metodi (comportamenti) degli oggetti

Un oggetto è un’istanza (un esemplare) di una classeUn programma può creare e usare uno o più oggetti (istanze) della stessa classe

---
## Class Structure

![[Pasted image 20240308174926.png|600]]

---
## Create a class in Java

>[!warning] oss
>- Ogni classe è memorizzata in un file separato
>- Il nome del file DEVE essere lo stesso della classe, con estensione .java

We can create a class in Java using the class keyword. For example,

```java
class ClassName {
  // fields
  // methods
}
```

Here, fields (variables) and methods represent the **state** and **behaviour** of the object respectively.
- fields are used to store data
- methods are used to perform some operations

For our bicycle object, we can create the class as

```java
class Bicycle {

  // state or field
  private int gear = 5;

  // behavior or method
  public void braking() {
    System.out.println("Working of Braking");
  }
}
```

Here, Bicycle is a prototype. Now, we can create any number of bicycles using the prototype. And, all the bicycles will share the fields and methods of the prototype.

>[!note] 
>We have used keywords `private` and `public`. These are known as access modifiers. To learn more, visit [[Java Access Modifiers]]

---
