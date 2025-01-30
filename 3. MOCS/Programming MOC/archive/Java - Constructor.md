---
created: 2024-03-08
type: Programming Note
programming language: "[[Java MOC]]"
related:
  - "[[Java OOP]]"
completed: false
updated: 2025-01-29T18:48
---
---

>[!info] Index
>1. [[#Introduzione]]
>2. [[#Types of Constructor]]
>	1. [[#No-Arg Constructor]]
>	2. [[#Parameterised Constructor]]
>	3. [[#Default Constructor]]
>3. [[#Constructor Overloading]]
>4. [[#How to "call" a constructor]]

---
## Introduzione 
- A constructor in Java is a "special" [[Java - Methods & Overloading|method]] that is invoked when an [[Java - Class and Objects|object]] of the [[Java - Class and Objects|class]] is created.
- Inizializzano i campi dello stato iniziale di un oggetto

>[!warning] Important Notes on Java Constructors
>- Constructors are invoked implicitly when you instantiate objects.
>- The two rules for creating a constructor are: 
>	1. The name of the constructor should be the same as the class.  
>	2. A Java constructor must not have a return type.
>- If a class doesn't have a constructor, the Java compiler automatically creates a **default constructor** during run-time. The default constructor initializes instance variables with default values. For example, the `int` variable will be initialized to `0`

---
## Types of Constructor

In Java, constructors can be divided into three types:

- [[#No-Arg Constructor]]
- [[#Parameterised Constructor]]

---
### No-Arg Constructor
Similar to methods, a Java constructor may or may not have any parameters (arguments).

```java
public class Counter {
	// Costruttore
	public Counter() {
		valore = 0;
	}
}
```

If a constructor does not accept any parameters, it is known as a no-argument constructor. For example,

---
### Parameterised Constructor
A Java constructor can also accept one or more parameters. 

```java
class Main {

  String languages;

  // constructor accepting single value
  Main(String lang) {
    languages = lang;
  }

  public static void main(String[] args) {

    // call constructor by passing a single value
    Main obj1 = new Main("Java");
    Main obj2 = new Main("Python");
    Main obj3 = new Main("C");
  }
}
```


---
### Default Constructor
If we do not create any constructor, the Java compiler automatically creates a no-arg constructor during the execution of the program.

```java
class Main {

  int a;
  boolean b;

  public static void main(String[] args) {

    // calls default constructor
    Main obj = new Main();

    System.out.println("Default Value:");
    System.out.println("a = " + obj.a);    // output: 0
    System.out.println("b = " + obj.b);    // output: false
  }
```

The default constructor initialises any uninitialised instance variables with default values.

|Type|Default Value|
|---|---|
|`boolean`|`false`|
|`byte`|**0**|
|`short`|**0**|
|`int`|**0**|
|`long`|**0L**|
|`char`|`\u0000`|
|`float`|**0.0f**|
|`double`|**0.0d**|
|`object`|`Reference null`|

---
## Constructor Overloading 

Similar to [Java method overloading](https://www.programiz.com/java-programming/method-overloading), we can also create two or more constructors with different parameters. This is called constructor overloading.

Esempio più metodi costruttori nella stessa classe:
```java
public Counter(){
	value = 0;
}

public Counter(int initaliaValue){
	value = initialValue;
}
```

---
## How to "call" a constructor

I **costruttori** vengono "chiamati" utilizzando `new NomeCostruttore()`
```java
static public void main(String[] args)
{
	Counter contatore1 = new Counter();
	Counter contatore2 = new Counter(42);
}

```

---