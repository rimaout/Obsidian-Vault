---
created: 2024-03-07
type: Programming Note
programming language: "[[Java MOC]]"
related:
  - "[[Java Strings]]"
completed: false
updated: 2024-05-27T13:29
---
---

>[!info] Index
>1. [[#`length()`]]
>2. [[#`toLowerCase()`]]
>3. [[#`toUpperCase()`]]
>4. [[#`charAt()`]]
>5. [[#`substring()`]]
>6. [[#`concat()`]]

>[!danger]
[[Java String Builder]]

---
## `length()`

**Description:**  
The `length()` method returns the length of a `String` object. The length is equal to the number of 16-bit Unicode characters in the string.

**Syntax:**  
```java
int length = string.length();
```

**Parameters:**  
The `length()` method does not take any parameters.

**Return Value:**  
This method returns an `int` value representing the number of characters in the `String`.

**Example:**
```java
String str = "Hello, world!";

int len = str.length();   // 13

```

---
## `toLowerCase()`

**Description:**  
The `toLowerCase()` method converts all the characters in a `String` to lower case.

**Syntax:**  
```java
String lowerCaseString = string.toLowerCase();
```

**Parameters:**  
The `toLowerCase()` method does not take any parameters.

**Return Value:**  
This method returns a `String` that represents the original string converted to lowercase.

**Example:**
```java
String str = "Hello, World!";
String lowerCaseStr = str.toLowerCase();    // "hello, world!"
```

---
## `toUpperCase()`

**Description:**  
The `toUpperCase()` method converts all the characters in a `String` to upper case.

**Syntax:**
```java
String upperCaseString = string.toUpperCase();
```

**Parameters:**  
The `toUpperCase()` method does not take any parameters.

**Return Value:**  
This method returns a `String` that represents the original string converted to uppercase.

**Example:**
```java
String str = "Hello, World!";

String upperCaseStr = str.toUpperCase();    // "HELLO, WORLD!"
```

---
## `charAt()`

**Description:**  
The `charAt()` method returns the character at the specified index in a `String`. The index value should lie between `0` and `length()-1`.

**Syntax:**  
```java
char ch = string.charAt(index);
```

**Parameters:**
The `charAt()` method takes one parameter:
- `index` (required): This is the index of the character that you want to retrieve. Indexing starts from `0`.

**Return Value:**  
This method returns the `char` value at the specified index of this string. The first `char` value is at index `0`.

**Example:**

```java
String str = "Hello, world!";
char ch = str.charAt(7);    // 'w'
```

---
## `substring()`

**Description:**  
The `substring()` method returns a new string that is a substring of the original string. The substring begins with the character at the specified index and extends to the end of the string or up to endIndex - 1, if the second argument is given.

**Syntax:**  
```java
String sub = string.substring(beginIndex); // or
String sub = string.substring(beginIndex, endIndex);
```

**Parameters:**  
The `substring()` method takes one or two parameters:

- `beginIndex` (required): This is the beginning index, inclusive.
- `endIndex` (optional): This is the ending index, exclusive.

**Return Value:**  
This method returns a new `String` that is a substring of this string.

**Example:**

```java
String str = "Hello, world!";
String subStr1 = str.substring(7);     // "world!"
String subStr2 = str.substring(0, 5);  // "Hello"

```

In `subStr1`, we only provide the `beginIndex`, so the substring includes all characters from index `7` to the end of the string.

In `subStr2`, we provide both `beginIndex` and `endIndex`, so the substring includes characters from index `7` up to but not including index `12`.

---
## `concat()`

**Description:**  
The `concat()` method concatenates the specified string to the end of this string. If the length of the argument string is `0`, then the original string is returned.

**Syntax:**  
```java
String concatenatedString = string.concat(s);
```

**Parameters:**  
The `concat()` method takes one parameter:

- `s` (required): This is the `String` that is concatenated to the end of this `String`.

**Return Value:**  
This method returns a `String` that represents the concatenation of this `String` object and the `String` argument.

**Example:**
```java
String str1 = "Hello, ";
String str2 = "world!";
String concatenatedStr = str1.concat(str2);    // "Hello, world!"
```

>[!warning] Differences between concat() and +
>The `concat()` method and the `+` operator both concatenate strings in Java, but there are some differences:
>
>1. **Performance:** For concatenating a few strings, there's not much difference in performance between `concat()` and `+`. However, if you're concatenating many strings in a loop, using `StringBuilder` or `StringBuffer` is more efficient.
> 
>2. **Null Handling:** If you use `concat()` and one of the strings is `null`, a `NullPointerException` will be thrown. On the other hand, if you use `+` and one of the strings is `null`, it will be treated as `"null"`.

---

## `indexOf()`

**Description:**  
The `indexOf()` method returns the index within this string of the first occurrence of the specified character. If a character with value `c` occurs in the character sequence represented by this `String` object, then the index of the first such occurrence is returned.

**Syntax:**  
```java
int index = string.indexOf(c);
```

**Parameters:**  
The `indexOf()` method takes one parameter:
- `c` (required): This is the character for which to find the first occurrence.

**Return Value:**  
This method returns the index of the first occurrence of the character in the character sequence, or `-1` if the character does not occur.

**Example:**
```java
String str = "Hello, world!";
int index = str.indexOf('w');    // 7
```

---
## `replace()`

**Description:**  
The `replace()` method returns a new string resulting from replacing all occurrences of oldChar in this string with newChar.

**Syntax:**  
```java
String replacedString = string.replace(oldChar, newChar);
```

**Parameters:**  
The `replace()` method takes two parameters:
- `oldChar` (required): This is the old character.
- `newChar` (required): This is the new character.

**Return Value:**  
This method returns a new `String` derived from this `String` by replacing every occurrence of `oldChar` with `newChar`.

**Example:**
```java
String str = "Hello, world!";
String replacedStr = str.replace('o', 'a');   // "Hella, warld!"
```

---
## `equals()`

**Description:**  
The `equals()` method compares this string to the specified object. The result is `true` if and only if the argument is not `null` and is a `String` object that represents the same sequence of characters as this object.

**Syntax:**  
```java
boolean isEqual = string1.equals(string2);
```

**Parameters:**  
The `equals()` method takes one parameter:
- `string2` (required): This is the `String` to compare with `string1`.

**Return Value:**  
This method returns a `boolean` - `true` if the given object represents a `String` equivalent to this string, `false` otherwise.

**Example:**

```java
String str1 = "Hello, world!";
String str2 = "Hello, world!";
boolean isEqual = str1.equals(str2);    // true
```

>[!warning] Differences between equals() and ==
>In Java, `equals()` and `==` operator are used for comparison. However, they work differently when it comes to objects like `String`.
>
>- `equals()`: This method compares the "content" of the strings. If two strings contain the same characters in the same order, `equals()` will return `true`.
>
>- `==` operator: This compares the "references" of the strings, not their content. It checks if both strings point to the same object in memory. So, even if two strings contain exactly the same characters, `==` will return `false` if they are not the same object in memory.
>
>Therefore, when comparing `String` values in Java, it's generally recommended to use `equals()`, not `==`.

---