---
created: 2024-03-05
type: Programming Note
programming language: "[[Java MOC]]"
related:
  - "[[Java built-in data types]]"
completed: true
updated: 2024-05-27T13:29
---
---

>[!info] Index
>1. [[#Type Casting]]
>2. [[#Explicit conversion]]
>3. [[#Implicit Type Casting]]
>4. [[#Explicit Type Casting]]
>5. [[#Examples]]

---
## Type Casting

The process of converting the value of one data type (`int`, `float`, `double`, etc.) to another data type is known as typecasting.

In Java, there are 13 types of type conversion. However, in this tutorial, we will only focus on the major 2 types.

1. [[#Explicit conversion]]
2. [[#Implicit Type Casting]]
3. [[#Explicit Type Casting]]

To learn about other types of type conversion, visit [Java Type Conversion (official Java documentation)](https://docs.oracle.com/javase/specs/jls/se10/html/jls-5.html "Java Type Conversion (official Java documentation)").

---
## Explicit conversion
Using a method that takes an argument of one type and returns a value of another type

Some of this methods are:
- `Integer.parseInt()`
- `Double.parseDouble()`
- `Integer.toString()`
- `Math.round()`
- `Math.floor()`
- `Math.ceil()`

---
## Implicit Type Casting

Java automatically converts one data type to another data type.

**Converting int to double**

```java

// create int type variable
int num = 10;
    System.out.println("The integer value: " + num);

// convert into double type
double data = num;
System.out.println("The double value: " + data);

// Output:
// The integer value: 10
// The double value: 10.0
```

Here, the Java first converts the `int` type data into the `double` type. And then assign it to the `double` variable.

>[!tip]
>In the case of Implicit Type Casting, the **lower data type** (having smaller size) is **converted** into the **higher data type** (having larger size). Hence there is no loss in data. This is why this type of conversion happens automatically.

---
## Explicit Type Casting

In **Explicit Type Casting**, we manually convert one data type into another using the parenthesis.

 Example: Converting double into an int
 
```java
// create double type variable
double num = 10.99;
System.out.println("The double value: " + num);

// convert into int type
int data = (int)num;
System.out.println("The integer value: " + data);

// Output:
// The double value: 10.99
// The integer value: 10
```

In the above example, we are assigning the `double` type variable named num to an `int` type variable named data.

Notice the line,

```
int data = (int)num;
```

Here, the `int` keyword inside the parenthesis indicates that that the num variable is converted into the `int` type.

In the case of **Narrowing Type Casting**, the higher data types (having larger size) are converted into lower data types (having smaller size). Hence there is the loss of data. This is why this type of conversion does not happen automatically.

---
## Examples 

| Expressions                | Type   | Value  |
| -------------------------- | ------ | ------ |
| `(int)2.71828`             | int    | 2      |
| `Math.round(2.71828)`      | long   | 2      |
| `(int)Math.round(2.71828)` | int    | 2      |
| `(int)Math.round(3.14159)` | int    | 3      |
| `Integer.parseInt("42")`   | int    | 42     |
| `"42" + 99`                | String | “4299” |
| `42 * 0.4`                 | double | 16.8   |
| `(int)42 * 0.4`            | double | 16.8   |
| `42 * (int)0.4`            | int    | 0      |
| `(int)(42 * 0.4)`          | int    | 16     |

---