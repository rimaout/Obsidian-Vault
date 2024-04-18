---
Created: 2024-03-07
Type: Programming Note
Programming Language: "[[Java MOC]]"
Related:
  - "[[Java Strings]]"
  - "[[Java Strings Methods]]"
Completed: true
---
---

>[!info] Index
>1. [[#`StringBuilder`]]
>2. [[#`append()`]]
>3. [[#`insert()`]]

---
## `StringBuilder`

**Package:** `java.lang`

**Description:**  
`StringBuilder` is a mutable sequence of characters. It is part of the `java.lang` package. It is like `String`, but can be modified. It is efficient for concatenating multiple strings together.

it can be used toughener with:
- [[#`append()`]]
- [[#`insert()`]]

---
## `append()`

**Description:**  
The `append()` method appends the string representation of the given argument to the sequence.

**Syntax:**  
```java
StringBuilder sb = new StringBuilder();
sb.append(s);
```

**Parameters:**  
The `append()` method takes one parameter:
- `s` (required): This is the `String` that is appended to the end of this `StringBuilder`.

**Return Value:**  
This method returns a reference to this object to enable chaining of calls to methods.

**Example:**
```java
StringBuilder sb = new StringBuilder("Hello, ");
String str = "world!";
sb.append(str);    // "Hello, world!"
```

---
## `insert()`

**Description:**  
The `insert()` method inserts the string representation of the second argument into the sequence at the specified position.

**Syntax:**

```java
StringBuilder sb = new StringBuilder();
sb.insert(index, s);
```

**Parameters:**  
The `insert()` method takes two parameters:
- `index` (required): This is the position at which to insert the second argument.
- `s` (required): This is the `String` that is inserted.

**Return Value:**  
This method returns a reference to this object to enable chaining of calls to methods.

**Example:**
```java

StringBuilder sb = new StringBuilder("Hello, world!");
String str = " beautiful";
sb.insert(7, str);    // "Hello, beautiful world!"
```

---