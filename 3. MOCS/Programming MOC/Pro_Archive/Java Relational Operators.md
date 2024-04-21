---
Created: 2024-03-05
Type: Programming Note
Programming Language: "[[Java MOC]]"
Related:
  - "[[Java Operators]]"
Completed: true
---
---

>[!info] Index
>1. [[#Java Relational Operators]]
>2. [[#Relational Operators with Numbers]]
>3. [[#Relational Operators with Characters]]
>4. [[#Relational Operators with Strings]]

---
## Java Relational Operators

Relational operators are used to check the relationship between two operands and return a `boole` value

``` java
// check if a is less than b
a < b;
```

Here, `<` operator is the relational operator. It checks if a is less than b or not.
It returns either `true` or `false`.

|Operator|Description|Example|
|---|---|---|
|`==`|Is Equal To|`3 == 5` returns **false**|
|`!=`|Not Equal To|`3 != 5` returns **true**|
|`>`|Greater Than|`3 > 5` returns **false**|
|`<`|Less Than|`3 < 5` returns **true**|
|`>=`|Greater Than or Equal To|`3 >= 5` returns **false**|
|`<=`|Less Than or Equal To|`3 <= 5` returns **true**|

---
### Relational Operators with Numbers

Relational operators can be used to compare numeric values:

```java
int a = 10, b = 5;

System.out.println(a == b); // false
System.out.println(a != b); // true
System.out.println(a > b); // true
System.out.println(a < b); // false
System.out.println(a >= b); // true
System.out.println(a <= b); // false
```

---
### Relational Operators with Characters

Relational operators can also be used to compare characters. Characters are internally represented as Unicode code points, so the comparison is based on their numeric values:

```java
char a = 'a', b = 'B';

System.out.println(a == b); // false
System.out.println(a != b); // true
System.out.println(a > b); // false
System.out.println(a < b); // true
System.out.println(a >= b); // false
System.out.println(a <= b); // true
```

---
### Relational Operators with Strings

Relational operators cannot be directly applied to strings as they are with numeric types. Instead, the `compareTo()` or `equals()` methods should be used to compare strings. 

The `compareTo()`method returns an integer value that indicates the relationship between the two strings:
- If `a.compareTo(b) > 0`, then `a` is greater than `b`.
- If `a.compareTo(b) < 0`, then `a` is less than `b`.
- If `a.compareTo(b) == 0`, then `a` is equal to `b`.

The `equals()`method returns a boolean value that indicates the relationship between the two strings:
- If `a.equals(b) == True`, then `a` is equal to `b`.
- If `a.equals(b) == False`, then `a` is not equal to `b`.

Read [[Java Strings]] to learn more.

Example:
```java
String a = "Hello";
String b = "World";

int result = a.compareTo(b);

if (result > 0) {
  System.out.println("a is greater than b");
} else if (result < 0) {
  System.out.println("a is less than b");
} else {
  System.out.println("a is equal to b");
}
```

Output:

```plaintext
a is less than b
```

---