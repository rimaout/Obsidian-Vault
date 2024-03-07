---
Created: 2024-03-03
Type: Programming Note
Programming Language: "[[Java MOC]]"
Related:
  - "[[Java Operators]]"
Completed: true
---
---
>[!info] Index:
>1. [[#Arithmetic Operators]]
>2. [[#Arithmetic Operators on Numbers]]
>3. [[#Arithmetic Operators on Chars]]
>4. [[#Arithmetic Operators on Strings]]
>	- [[#Concatenation with `+` Operator]]
>	- [[#Concatenation of Strings with Other Data Types]]
>	- [[#Implicit Conversion in Concatenation]]
>	- [[#Special Case Concatenation Order Matters]]

---
## Arithmetic Operators

Arithmetic operators are used to perform arithmetic operations on variables and data. For example,

```
a + b;
```

Here, the `+` operator is used to add two variables a and b. Similarly, there are various other arithmetic operators in Java.

|   |   |
|---|---|
|Operator|Operation|
|`+`|Addition|
|`-`|Subtraction|
|`*`|Multiplication|
|`/`|Division|
|`%`|Modulo Operation (Remainder after division)|

---
## Arithmetic Operators on Numbers

```java

int a = 12, b = 5;

a + b    // 17

a - b    // 7

a * b    // 60

a / b    // 2 

a % b    // 2
```

>[!warning] Division Operator
>- Division two integers --> Result: integer
>- Division floating-point with at least one floating-point  --> Result: floating-point
>
>```java
>(9 / 2) is 4
>(9.0 / 2) is 4.5
>(9 / 2.0) is 4.5
>(9.0 / 2.0) is 4.5
>```
>
>```java
>int a = 9;
>int b = 2;
>
> System.out.println(a/b);             // output: 4
> System.out.println((float)(a/b));    // output: 4.0
> System.out.println((float)(a)/b);    // output: 4.5
>```
 
---
## Arithmetic Operators on Chars

When you perform an arithmetic operation on a `char`, it gets implicitly cast to an `int` value. This `int` value corresponds to the Unicode value of the character.

Here's an example:
```java
public class Main {

    public static void main(String[] args) {

		char a = 'z';   // Unicode value: 122
        char b = '!';   // Unicode value: 33
    
        int  r1 = a-b;  // 89
        char r2 = a+b;  // ERROR: incompatible types
        char r3 = (char)(a-b);    // 'Y'
        
        int  r4 = a+1;   // 123
        char r5 = a+1;   // ERROR: incompatible types
        char r6 = (char)(a+1);   // '{'
    }
}
```

---
## Arithmetic Operators on Strings

In Java, strings are objects that represent sequences of characters. The Java platform provides the `String` class to create and manipulate strings. While arithmetic operators like `+`, `-`, `*`, `/`, and `%` are not directly applicable in the same way as they are with numeric data types, the `+` operator can be used with strings, but it behaves differently. It is used for concatenation, which means joining strings together end-to-end to create a new string.

### Concatenation with `+` Operator

```java
String a = "Hello, ";
String b = "world!";

String c = a + b;  // "Hello, world!"
```

The `+` operator can also be used to concatenate strings with other data types. When one of the operands is a string, the `+` operator concatenates the string representation of the other operand.

```java
String str = "Year: ";
int year = 2023;

String result = str + year;  // "Year: 2023"
```

---
### Implicit Conversion in Concatenation

When using the `+` operator with mixed data types where at least one operand is a string, Java automatically converts the other operand to its string representation before concatenation.

```java
String message = "Score: " + 100;  // "Score: 100"
```

In this case, the integer `100` is automatically converted to the string `"100"` before it is concatenated with the string `"Score: "`.

---
### Special Case: Concatenation Order Matters

When concatenating strings with other types in a single expression, the result might depend on the order and grouping of the operations due to how expressions are evaluated from left to right.

```java
System.out.println("Sum: " + 10 + 20);  // "Sum: 1020"
System.out.println("Sum: " + (10 + 20));  // "Sum: 30"
```

In the first line, the string `"Sum: "` is concatenated with `10` resulting in `"Sum: 10"`, which is then concatenated with `20`, resulting in the string `"Sum: 1020"`. In the second example, because of the parentheses, `10 + 20` is evaluated first, resulting in `30`, which is then concatenated with `"Sum: "`, producing the expected result of `"Sum: 30"`.


---
### Concatenation of Characters and Strings

In Java, the `char` data type represents a single character. Unlike strings, when you try to concatenate two `char` values using the `+` operator, the result is not a string concatenation but a numeric addition, because `char` values are treated as integers. 

```java
char a = 'A'; // Unicode value: 65
char b = 'B'; // Unicode value: 66

int result2 = a + b;  // 131, not "AB"
String result1 = a + b; // error: incompatible types

```

To concatenate `char` values as strings, you can prepend or append an empty string (`""`) to the expression. This forces Java to treat the operation as string concatenation rather than numeric addition.

```java
char a = 'A';
char b = 'B';

String result = "" + a + b;  // "AB"
```

---
