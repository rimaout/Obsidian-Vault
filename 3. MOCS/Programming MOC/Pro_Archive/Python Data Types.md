---
Created: 2022-03-02
Type: Programming Note
Programming Language: "[[Python MOC]]"
Related: []
Completed: true
---
---
## Index
1. [[#Introduction]]
2. [[#Python Casting]]
3. [[#Mutable and Unmutable data types]]
4. [[#Ordered and Unordered data types]]


---
## Introduction

Variables can store data of different types, and different types can do different things.

Python has the following data types built-in by default, in these categories:

| Text Type: | str |
| --- | --- |
| Numeric Types: | int, float,complex |
| Sequence Types: | list, tuple, range |
| Mapping Type: | dict |
| Set Types: | set, frozenset |
| Boolean Type: | bool |
| Binary Types: | bytes, bytearray, memoryview |
| None Type: | NoneType |

| Example | Data Type |
| --- | --- |
| x = "Hello World" | str |
| x = 20 | int |
| x = 20.5 | float |
| x = 1j | complex |
| x = ["apple", "banana", "cherry"] | list |
| x = ("apple", "banana", "cherry") | tuple |
| x = range(6) | range |
| x = {"name" : "John", "age" : 36} | dict |
| x = {"apple", "banana", "cherry"} | set |
| x = frozenset({"apple", "banana", "cherry"}) | frozenset |
| x = True | bool |
| x = b"Hello" | bytes |
| x = bytearray(5) | bytearray |
| x = memoryview(bytes(5)) | memoryview |
| x = None | NoneType |

You can get the data type of any object by using the `type()` function:

```python
x = 5
print(type(x)) #Output: <class 'int'>
```

---

##  Python Casting
![[ Python Casting]]

---
## Mutable and  Unmutable data types
An unmutable datatype can't be modified, it can be only copied, rewritten and deleted.

**Unmutable data types:**
- [[Python Strings|Strings]]
- [[Python Tuples|Tuples]]
- [[Python Numbers|Numbers]]
- [[Python Booleans|Booleans]]
- [[Python Bytes|Bytes]]

- Frozen Sets

**Mutable data types:**
- [[Python Lists|Lists]]
- [[Python Dictionaries|Dictionaries]]
- [[Python Sets|Sets]]

**oss:**
- Immutable objects are common in [functional programming](https://realpython.com/python-functional-programming/), while mutable objects are widely used in [object-oriented programming](https://realpython.com/python3-object-oriented-programming/). 
- - Because Python is a multiparadigm programming language, it provides mutable and immutable objects for you to choose from when solving a problem.

---

## Ordered and Unordered data types
An unordered datatype can't iterated, this means that [[Python Index]], [[Python Slicing]], [[Python For Loops|for]], [[Python While Loops|while]] loops don't work on unordered data types

**Unordered data types:**
- [[Python Numbers|Numbers]]
- [[Python Sets|Sets]]
- [[Python Dictionaries|Dictionaries]]
- [[Python Booleans|Booleans]]

**Ordered data types:**
- [[Python Strings|Strings]]
- [[Python Tuples|Tuples]]
- [[Python Lists|Lists]]

---