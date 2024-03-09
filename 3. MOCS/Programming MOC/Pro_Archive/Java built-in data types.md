---
Created: 2024-03-01
Type: Programming Note
Programming Language: "[[Java MOC]]"
Related: 
Completed: true
---
---
## Java data types

- Data types specify the type of data that can be stored inside [[Java Variables]].
- Java is a **statically-typed language**. This means that all variables must be declared before they can be used.

Java has 9 built-in data types:
- 8 [[#Primitive Data Types]] + [[#String type]]

---
## Primitive Data Types

There are 8 different primitive data types:
1. [[#boolean type]]
2. [[#byte type]]
3. [[#short type]]
4. [[#int type]]
5. [[#long type]]
6. [[#double type]]
7. [[#float type]]
8. [[#char type]]

| Tipo             | Operatori |      Esempio      | Intervallo                               | Space  |
| ---------------- | :-------: | :---------------: | ---------------------------------------- | ------ |
| `byte`           | + - * / % |      27 + 1       | -128…127                                 | 1 byte |
| `short`          | + - * / % |      27 + 1       | -32768...32767                           | 2 byte |
| <u>`int`</u>     | + - * / % |      27 + 1       | -2147483648…2147483647                   | 4 byte |
| `long`           | + - * / % |      27 + 1       | -1e9…1e9                                 | 8 byte |
| `float`          | + - * / % |  3.14 * 5.01e23   | 7 cifre decimali significative           | 4 byte |
| <u>`double`</u>  | + - * / % |  3.14 * 5.01e23   | 15 cifre decimali significative          | 8 byte |
| <u>`boolean`</u> | && \|\| ! |  true \|\| false  | true, false                              | 1 byte |
| <u>`char`</u>    |    + -    |        ‘a’        | Tutti i caratteri codificati con unicode | 2 byte |
| <u>`String`</u>  |    + -    | “Hello” + “World” |                                          |        |
|                  |           |                   |                                          |        |

**oss:** Strings are not primitive data types

---
### boolean type

- The `boolean` data type has two possible values, either `true` or `false`.
- Default value: `false`

```java
class Main {
  public static void main(String[] args) {
    	
    boolean flag = true;
    System.out.println(flag);    // prints true
  }
}
```

---
### byte type

- The `byte` data type can have values from **-128** to **127** (8-bit signed two's complement integer).
- If it's certain that the value of a variable will be within -128 to 127, then it is used instead of int to save memory.
- Default value: 0

```java
class Main {
  public static void main(String[] args) {

    byte range;
    range = 124;
    System.out.println(range);    // prints 124
  }
}
```

---
### short type

- The `short` data type in Java can have values from **-32768** to **32767** (16-bit signed two's complement integer).
- If it's certain that the value of a variable will be within -32768 and 32767, then it is used instead of other integer data types (`int`, `long`).
- Default value: 0

```java
class Main {
  public static void main(String[] args) {
    	
    short temperature;
    temperature = -200;
    System.out.println(temperature);  // prints -200
  }
}
```

---
### int type

- The `int` data type can have values from $-2^{31}$ to $2^{31}-1$ (32-bit signed two's complement integer).
- Default value: 0

```java
class Main {
  public static void main(String[] args) {
    	
    int range = -4250000;
    System.out.println(range);  // print -4250000
  }
}
```

---
### long type

- The long data type can have values from $-2^{63}$ to $2^{63}-1$ (64-bit signed two's complement integer).
- Default value: 0

>[!warning]
>You must write the literal with the **f** ant the and
>```java
 >long a = 84489094021L;
 >long b = 84489094021;   // integer number too large
 >
 >// when you don't put a L at the end of the number it is casted to a int
>```

```java
class LongExample {
  public static void main(String[] args) {
    	
    long range = -42332200000L;
    System.out.println(range);    // prints -42332200000
  }
}
```

Notice, the use of `L` at the end of `-42332200000`. This represents that it's an integer of the `long` type.

---
### double type

- The `double` data type is a double-precision 64-bit [[Numeri binari con virgola mobile (floating point)|floating point]].
- It should never be used for precise values such as currency.
- Default value: 0.0 (0.0d)

```java
class Main {
  public static void main(String[] args) {
    	
    double number = -42.3;
    System.out.println(number);  // prints -42.3
  }
}
```

---
### float type

- The float data type is a single-precision 32-bit [[Numeri binari con virgola mobile (floating point)|floating point]].
- It should never be used for precise values such as currency.
- Default value: 0.0 (0.0f)

>[!warning]
>You must write the literal with the **f** ant the and
>```java
 >float a = 12.2f;
 >float b = 12.3;    // Error: incompatible types
>```

```java
class Main {
  public static void main(String[] args) {
    	
    float number = -42.3f;
    System.out.println(number);  // prints -42.3
  }
}
```

Notice that we have used -42.3f instead of -42.3in the above program. It's because -42.3 is a double literal.

To tell the compiler to treat -42.3 as float rather than double, you need to use f or F.

---
### char type

- It's a 16-bit [[Unicode]] character.
- The minimum value of the char data type is `'\u0000'` (0) and the maximum value of the is `'\uffff'`.
- Default value: `'\u0000'`

```java
class Main {
  public static void main(String[] args) {
    	
    char letter = '\u0051';
    System.out.println(letter);  // prints Q

	char letter1 = '9';
    System.out.println(letter1);  // prints 9
    	
    char letter2 = 65;
    System.out.println(letter2);  // prints A
  }
}
```

---
## String type

Java also provides support for character strings via `java.lang.String class`. Strings in Java are not primitive types. Instead, they are objects. 

```java
String myString = "Java Programming";
```

Here, `myString` is an object of the `String` class. To learn more, visit [[Java Strings]].

---