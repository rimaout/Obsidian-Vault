---
created: 2022-03-02
type: Programming Note
programming language: "[[Python MOC]]"
related: 
completed: true
updated: 2024-10-03T16:19
---
---
# Index
1. [[#Introduction]]
2. [[#raw-string]]
3. aritmetic operators
4. comparison operators
5. index
6. slicing
7. loops
8. [[#Built-in functions]]


---
# Introduction

**Strings main characteristics:**
1. *Contained by quotes:* Strings are defined within single(') or double quotes(").
2. *Sequence of characters:* A string is a sequence of characters, meaning they can contain text characters, numbers, special symbols, and more.
3. *Iterable Object:* can be divided in samller parts
4. *Immutable:** a string is an immutable object, which means that once you create a string object, you cannot modify its contents.
5. *Ordinated:* admits the repetition of elements and can be [sliced](Python%20Slicing.md) and indexed


    ```python
    string = "hello"
    string[0] = "H"    # Output: error (you can't change a string)
    ```

---

---
## raw-string
![[Python Raw String]]


---
## Concatenation and Replication
[[Python Operators]]
>[!warning] Note:
>A string is an **immutable object**, which means that when you concatenate two strings you are creating a new one

| Operator | Description | Example |
| --- | --- | --- |
| + | Concatenate two strings | "hello" + "world" -> "hello world" |
| * | Repeat a string for a certain number of times | "spam" * 3 -> "spamspamspam" |

---

## [Comparison  Operators](Python%20Comparison%20Operators])

In Python, you can compare two strings using comparison operators. The comparison operators return a Boolean value (`True` or `False`) depending on whether the comparison is true or false. 

The comparison operators available for strings are:

1. `==` (equal to): returns `True` if the two strings are equal, and `False` otherwise.
2. `!=` (not equal to): returns `True` if the two strings are not equal, and `False` otherwise.
3. `<` (less than): returns `True` if the first string comes before the second string in alphabetical order, and `False` otherwise.
4. `>` (greater than): returns `True` if the first string comes after the second string in alphabetical order, and `False` otherwise.
5. `<=` (less than or equal to): returns `True` if the first string comes before or is equal to the second string in alphabetical order, and `False` otherwise.
6. `>=` (greater than or equal to): returns `True` if the first string comes after or is equal to the second string in alphabetical order, and `False` otherwise.
7. `in`: returns `True` if a substring is found within a string, and `False` otherwise.
8. `not in`: returns `True` if a substring is not found within a string, and `False` otherwise.

Here are some examples:

```python
str1 = "apple"
str2 = "banana"

print(str1 == str2)  # Output: False
print(str1 != str2)  # Output: True
print(str1 < str2)   # Output: True
print(str1 > str2)   # Output: False
print(str1 <= str2)  # Output: True
print(str1 >= str2)  # Output: False

str3 = "Hello, World!"
str4 = "World"
str5 = "Python"

print(str4 in str3)   # Output: True
print(str5 in str3)   # Output: False
print(str4 not in str3)   # Output: False
print(str5 not in str3)   # Output: True
```

>[!warning] Note:
 Note that when comparing strings, Python uses **lexicographical order**, which means it compares the ASCII values of the characters in the strings.

---
## Built-in functions

Python offers numerous built-in functions for working with strings. Here are some of the most commonly used functions:

#### `len()`

The `len()` function returns the length of the string. For example:

```python
my_string = "Hello, World!"
print(len(my_string)) # Output: 13
```

#### `str()`

The `str()` function converts a value to a string. For example:

```
my_number = 42
my_string = str(my_number)
print(my_string) # Output: "42"
```

#### `count()`

The `count()` function counts the number of occurrences of a substring within a string. For example:

```
my_string = "Hello, World!"
print(my_string.count("l")) # Output: 3
```

#### `join()`

The `join()` function joins a list of strings into a single string using a specific separator. For example:

```python
my_list = ["apple", "banana", "cherry"]
print(", ".join(my_list)) # Output: "apple, banana, cherry"
```

#### `split()`

The `split()` function splits a string into a list of strings using a specific separator. For example:

```python
my_string = "Hello, World!"
print(my_string.split(",")) # Output: ["Hello", " World!"]
```

#### `upper()` and `lower()`

The `upper()` and `lower()` functions convert a string to uppercase or lowercase letters. For example:

```python
my_string = "Hello, World!"
print(my_string.upper()) # Output: "HELLO, WORLD!"
print(my_string.lower()) # Output: "hello, world!"
```

#### `islower()` and `isupper()`

The `islower()` and `isupper()` functions return True if all characters in the string are lowercase or uppercase respectively, otherwise False. For example:

```python
my_string1 = "hello, world!"
my_string2 = "HELLO, WORLD!"
print(my_string1.islower()) # Output: True
print(my_string2.isupper()) # Output: True
```

#### `capitalize()`

The `capitalize()` function converts the first letter of a string to uppercase. For example:

```python
my_string = "hello world"
print(my_string.capitalize()) # Output: "Hello world"
```

#### `swapcase()`

The `swapcase()` function converts uppercase letters to lowercase and vice versa within a string. For example:

```python
my_string = "Hello, World!"
print(my_string.swapcase()) # Output: "hELLO, wORLD!"
```

#### `replace()`

The `replace()` function replaces a substring with another substring within a string. For example:

```python
my_string = "Hello, World!"
print(my_string.replace("World", "Python")) # Output: "Hello, Python!"
```

#### `find()`

The `find()` function returns the index of the first occurrence of a substring within a string, or -1 if the substring is not found. For example:

```python
my_string = "Hello, World!"
print(my_string.find("World")) # Output: 7
print(my_string.find("Python")) # Output: -1
```

#### `title()`

The `title()` function converts the first letter of each word to uppercase within a string. For example:

```python
my_string = "hello world"
print(my_string.title()) # Output: "Hello World"
```

#### `startswith()` and `endswith()`

The `startswith()` and `endswith()` functions check if a string starts or ends with a certain substring and return True or False. For example:

```python
my_string = "Hello, World!"
print(my_string.startswith("Hello")) # Output: True
print(my_string.endswith("World!")) # Output: True
```

#### `format()`

The `format()` function formats a string by inserting values into specified positional or named placeholders. For example:

```python
name = "Alice"
age = 30
print("My name is {} and I'm {} years old.".format(name, age)) # Output: "My name is Alice and I'm 30 years old."
```

#### `replace()`

The `replace()` function replaces a substring with another one within a string. For example:

```python
my_string = "Hello, World!"
print(my_string.replace("World", "Python")) # Output: "Hello, Python!"
```

---

### [[Slicing ]]of a string

>[!warning] Note:
>Slicing a string **does not modify the original string** - it returns a new string that contains only the specified portion of the original string, because *strings* are *immutable*

You can slice a string in Python using the syntax `string[start:end:step]`, where:

- `start` is the index of the first character you want to include in the slice
- `end` is the index of the first character you want to *exclude* from the slice
- `step` is the number of characters to skip between each character included in the slice

Here are some examples:

```python
string = "Hello, World!"

# slice the entire string
print(string[:])           # Output: Hello, World!

# slice from index 0 to index 5 (excluding 5)
print(string[0:5])         # Output: Hello

# slice from index 7 to the end
print(string[7:])          # Output: World!

# slice from index 2 to index 10, skipping every other character
print(string[2:10:2])      # Output: lo,W

# slice from the beginning to the end, skipping every other character
print(string[::2])         # Output: Hlo ol!

# slice from the end of the string to the beginning
print(string[::-1])        # Output: !dlroW ,olleH

# slice from the end of the string to index 2 (excluding 2), skipping every other character
print(string[-1:1:-2])     # Output: !lo le

# slice from index -5 (5th character from the end) to index -1 (excluding -1), skipping every other character
print(string[-5:-1:2])     # Output: Wo

# slice from index -10 (10th character from the end) to index -7 (excluding -7)
print(string[-10:-7])      # Output: orl

# slice from index -3 (3rd character from the end) to the end of the string
print(string[-3:])         # Output: ld!
```


>[!warning] Note:
>That you can mix positive and negative indices in a single slice, and you can omit any of the three parameters (`start`, `end`, and `step`) as needed. 

---

## [[Quartz Index Example]] of a string

In Python, a string is a sequence of characters, and you can access individual characters in the string by their position or index within the sequence.

- The index of a string starts at 0, which means that the first character in the string has an index of 0
- The second character has an index of 1, and so on.

```lua
  +---+---+---+---+---+
  | h | e | l | l | o |
  +---+---+---+---+---+
  | 0 | 1 | 2 | 3 | 4 |
  +---+---+---+---+---+
  |-5 |-4 |-3 |-2 |-1 |
  +---+---+---+---+---+
```

To access a specific character in a string, you can use its index within square brackets `[]`, like this:

```python
string = "hello"
print(string[0])   # Output: "h"
print(string[1])   # Output: "e"
print(string[2])   # Output: "l"
print(string[3])   # Output: "l"
print(string[4])   # Output: "o"

print(string[-5])   # Output: "h"
print(string[-4])   # Output: "e"
print(string[-3])   # Output: "l"
print(string[-2])   # Output: "l"
print(string[-1])   # Output: "o"
```

In this example, we access each character in the string `string` by its index within square brackets `[]`. 

>[!warning] Note:
>The index must be an integer, and it must be within the range of valid indices for the string (from 0 to `len(string) - 1`).  Otherwise, a `IndexError` will be raised.
---

## [[Loops]] in a string

In Python, a loop is a programming construct that allows you to iterate over a sequence of items, such as the characters in a string.

There are two types of loops in Python: the `for` loop and the `while` loop.

- we use a `for`  loop to iterate over each character in the string.
    
    ```python
    string = "hello"
    for char in string:
        print(char)
    ```
    
- `while`  loop is designed to repeat a block of code while a specific condition is true
    
    ```python
    string = "hello"
    index = 0
    while index < len(string):
        print(string[index])
        index += 1
    ```
    

---