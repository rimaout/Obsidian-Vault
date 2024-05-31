---
created: 2024-04-19T15:02
type: Programming Note
programming language: "[[Java MOC]]"
related:
  - "[[Java Strings]]"
completed: false
updated: 2024-05-27T13:29
---
---

>[!abstract] Index
>1. [[#Introduction]]
>2. [[#How to crate a string builder]]
>3. [[#String Builder Methods]]
>4. [[#Examples]]

>[!abstract] Related
>- [[Java Strings]]

---
## Introduction

In Java, `String` objects are immutable, which means once a `String` object is created, it cannot be changed. If you perform any operation that alters the `String`, like concatenation, a new `String` object is created in the memory. This can lead to inefficiency in terms of memory usage and performance, especially when dealing with large amounts of string manipulations in loops.

On the other hand, `StringBuilder` is mutable. It allows you to modify the string without creating new instances. This makes it a better choice for string manipulation operations, as it's more memory-efficient and faster.

---
## How to crate a string builder


In Java, you can create a `StringBuilder` object using the `StringBuilder` constructor.

```java
StringBuilder sb = new StringBuilder();
```

This creates an empty `StringBuilder` with an initial capacity of 16 characters.

If you want to initialise the `StringBuilder` with a specific string, you can pass the string to the constructor:
```java

StringBuilder sb = new StringBuilder("Hello, world!");
```
In this example, the `StringBuilder` is initialised with the string "Hello, world!".

You can also specify an initial capacity for the `StringBuilder`:
```java
StringBuilder sb = new StringBuilder(50);
```

In this example, the `StringBuilder` is created with an initial capacity of 50 characters. This can be useful if you know you'll be appending a large number of characters to the `StringBuilder`, as it can help to reduce the number of reallocations.

---
## String Builder Methods

The methods provided by the `StringBuilder` class in Java:

| Method                                                              | Info                                                                                                                                                                                                                                                            |
| ------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `StringBuilder()`                                                   | Constructs a string builder with no characters in it and an initial capacity of 16 characters                                                                                                                                                                   |
| `StringBuilder(CharSequence seq)`                                   | Constructs a string builder that contains the same characters as the specified `CharSequence`                                                                                                                                                                   |
| `StringBuilder(int capacity)`                                       | Constructs a string builder with no characters in it and an initial capacity specified by the `capacity` argument                                                                                                                                               |
| `StringBuilder(String str)`                                         | Constructs a string builder initialised to the contents of the specified string                                                                                                                                                                                 |
| `append(...)`                                                       | This method has many overloaded versions for different parameter types like `Object`, `String`, `CharSequence`, `char[]`, `boolean`, `char`, `int`, `long`, `float`, `double`, etc. It appends the string representation of the given parameter to the sequence |
| `insert(int offset, ...)`                                           | This method also has many overloaded versions for different parameter types. It inserts the string representation of the given parameter at the specified `offset`                                                                                              |
| `delete(int start, int end)`                                        | Removes the characters in a substring of this sequence                                                                                                                                                                                                          |
| `deleteCharAt(int index)`                                           | Removes the `char` at the specified position in this sequence                                                                                                                                                                                                   |
| `replace(int start, int end, String str)`                           | Replaces the characters in a part of this sequence with characters in the specified `String`                                                                                                                                                                    |
| `reverse()`                                                         | Reverses the sequence                                                                                                                                                                                                                                           |
| `setCharAt(int index, char ch)`                                     | Sets the character at the specified `index` to `ch`                                                                                                                                                                                                             |
| `substring(int start)`, `substring(int start, int end)`             | Returns a new `String` that contains a subsequence of characters currently contained in this sequence                                                                                                                                                           |
| `length()`                                                          | Returns the length (character count)                                                                                                                                                                                                                            |
| `setLength(int newLength)`                                          | Sets the length of the character sequence                                                                                                                                                                                                                       |
| `capacity()`                                                        | Returns the current capacity.                                                                                                                                                                                                                                   |
| `ensureCapacity(int minimumCapacity)`                               | Ensures that the capacity is at least equal to the specified minimum                                                                                                                                                                                            |
| `trimToSize()`                                                      | Attempts to reduce storage used for the character sequence                                                                                                                                                                                                      |
| `charAt(int index)`                                                 | Returns the `char` value in this sequence at the specified index                                                                                                                                                                                                |
| `indexOf(String str)`, `indexOf(String str, int fromIndex)`         | Returns the index within this string of the first occurrence of the specified substring                                                                                                                                                                         |
| `lastIndexOf(String str)`, `lastIndexOf(String str, int fromIndex)` | Returns the index within this string of the rightmost occurrence of the specified substring                                                                                                                                                                     |
| `toString()`                                                        | Returns a string representing the data in this sequence                                                                                                                                                                                                         |

---
## Examples

`StringBuilder` in Java has several useful methods. Here are some of them:

- `append()`: Adds the string representation of a specific data type to the sequence.
    ```java

    StringBuilder sb = new StringBuilder();
    
    sb.append("Hello, ");
    
    sb.append("world!");
	```    

- `insert()`: Inserts the string representation of a specific data type at the specified position.
	```java
     
    StringBuilder sb = new StringBuilder("Hello, world!");
    
    sb.insert(7, "beautiful ");
	```   
	
- `delete()`: Removes the characters in a substring of this sequence.
    ```java
    StringBuilder sb = new StringBuilder("Hello, beautiful world!");
    
    sb.delete(7, 17);
    ```

- `reverse()`: Causes this character sequence to be replaced by the reverse of the sequence.
    ```java
    StringBuilder sb = new StringBuilder("Hello, world!");
    
    sb.reverse();
    ```

- `toString()`: Returns a string representing the data in this sequence.
    ```java
    StringBuilder sb = new StringBuilder("Hello, world!");
    
    String str = sb.toString();
    ```

---