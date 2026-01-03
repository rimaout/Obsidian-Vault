---
created: 2024-02-28
type: Programming Note
programming language: "[[Java MOC]]"
related:
  - "[[Java Variables]]"
completed: true
updated: 2024-05-27T13:29
---
---

>[!info] Index
>1. [[#Java Literals]]
>2. [[#Boolean Literals]]
>3. [[#Integer Literals]]
>4. [[#Floating-point Literals]]
>5. [[#Character Literals]]
>6. [[#String literals]]

---
## Java Literals
Literals are data used for representing fixed values.

---
### Boolean Literals
In Java, boolean literals are used to initialise boolean data types. They can store two values: true and false.

```java
boolean flag1 = false;
boolean flag2 = true;
```

Here, `false` and `true` are two boolean literals.

---
### Integer Literals
An integer literal is a numeric value (associated with numbers) without any fractional or exponential part. 

There are 4 types of integer literals in Java:
1. binary (base 2)
2. decimal (base 10)
3. octal (base 8)
4. hexadecimal (base 16)

```java
// binary
int binaryNumber = 0b10010;
// octal 
int octalNumber = 027;

// decimal
int decNumber = 34;

// hexadecimal 
int hexNumber = 0x2F; // 0x represents hexadecimal
// binary
int binNumber = 0b10010; // 0b represents binary
```

>[!tip] 
>Integer literals are used to initialize variables of integer types like `byte`, `short`, `int`, and `long`.

---
### Floating-point Literals
A floating-point literal is a numeric literal that has either a fractional form or an exponential form. 

```java
class Main {
  public static void main(String[] args) {
    	
    double aDouble = 3.4;
    float aFloat = 3.4F;
 
    // 3.445*10^2
    double aDoubleScientific = 3.445e2;

    System.out.println(aDouble);  // prints 3.4
    System.out.println(aFloat);    // prints 3.4
    System.out.println(aDoubleScientific);   // prints 344.5
  }
}
```

>[!tip] 
>The floating-point literals are used to initialize `float` and `double` type variables.

---
### Character Literals
Character literals are Unicode character enclosed inside **single quotes**.

```java
char letter = 'a';
```

Here, `a` is the character literal.

>[!tip] 
>We can also use [[Escaping Sequences]] as character literals. For example, **\\b** (backspace), **\\t** (tab), **\\n** (new line), etc.


---
### String literals

A string literal is a sequence of characters enclosed inside **double-quotes**.

```java
String str1 = "Java Programming";
String str2 = "Ciao Mamma";
```

Here, `Java Programming` and `Ciao Mamma` are two string literals.

---