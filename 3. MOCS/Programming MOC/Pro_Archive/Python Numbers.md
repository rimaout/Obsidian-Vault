---
created: 2023-03-02
type: Programming Note
programming language: "[[Python MOC]]"
related: 
completed: true
updated: 2024-05-27T13:29
---
---
# Index
1. [[#Numbers]]
2. [[#Definition]]
3. [[#Type]]
	- [[#Int]]
	- [[#Float]]
	- [[#Complex]]
4.  [[#Type Conversion]]
5. [[#Operators]]
	- [[#Augmented Assignment Operators]]
	-  [[#Comparison Operators]]
	-  [[#Built-in Functions]]
	- [[#~~ Slicing of a Number~~]]
	- [[#~~ Index of a Number~~]]
	- [[#~~ Loops in a Number~~]]
6. [[#Random Module]]
7. [[#Math Module]]

---
# Definition

Numbers in python are considered **atomic data types**, which means they cannot be divided further into smaller elements.

This means that a number is **not iterable** so you can not loop, slice or index a number.


>[!warning] Oss:
>Iterable objecta access their elements one by one. For example, strings, lists, tuples, and sets are iterable objects in Python.
---

---
## Type

```python
Nuemro = 69420
```

There are three numeric types in Python:

- `int`
- `float`
- `complex`

```python
x = 1    # int
y = 2.8  # float
z = 1j   # complex
```

---
### Int

Int, or integer, is a whole number, positive or negative, without decimals, of unlimited length.

```python
x = 1
y = 35656222554887711
z = -3255522
```

---
### Float

Float, or "floating point number" is a number, positive or negative, containing one or more decimals.

```python
x = 1.10
y = 1.0
z = -35.59
```

Float can also be scientific numbers with an "e" to indicate the power of 10:

```python
x = 35e3 #Output: 35000.0
y = 12E4 #Output: 120000.0
```

---
### Complex

Complex numbers are written with a "j" as the imaginary part:

```python
x = 3+5j
y = 5j
z = -5j
```

---
## Type Conversion

You can convert from one type to another with the `int()`, `float()`, and `complex()` methods:

```python
x = 1    # int
y = 2.8  # float
z = 1j   # complex

#convert from int to float:
a = float(x) #Output: 1.0

#convert from float to int:
b = int(y) #Output: 2

#convert from int to complex:
c = complex(x) #Output: (1+0j)

#convert from float to complex:
d = complex(y) #Output: (2.8+0j)
```

>[!warning] Note:
>When converting from a float to an int, the decimal part will be will be rounded down 
>to the nearest whole number. For example, `int(2.8)` will output `2`, not `3`.
>
>Similarly, when converting from an int or float to a complex number, the imaginary part will be set to `0.`

---

## [[Python Operators]]

Python supports a variety of operators for performing arithmetic operations on numbers, such as `+`, `-`, `*`, `/`, `%` (modulo), `**` (exponentiation), and `//` (floor division). For example:

```python
x = 10
y = 3
print(x + y)  # Addition # Output: 13
print(x - y)  # subtraction   # Output: 7
print(x * y)  # multiplication  # Output: 30
print(x / y)  # division Output: 3.3333333333333335
print(x % y)  # modulo(rest) # Output: 1
print(x ** y) # power # Output: 1000
print(x // y) # floor division # Output: 3
```

---

## Augmented Assignment [[Python Operators]]

Augmented Assignment Operators in Python are shorthand operators that combine an arithmetic operator with an assignment operator. 

The following table shows the list of augmented assignment operators available in Python:
```python
x += 5    # equivalent to x = x + 5 |
x -= 5    # equivalent to x = x - 5 
x *= 5     # equivalent to x = x * 5 
x /= 5    # equivalent to x = x / 5 
x %= 5    # equivalent to x = x % 5 
x //= 5   # equivalent to x = x // 5 
x **= 5     # equivalent to x = x ** 5 
```

- These operators can be used with any numeric data type, such as integers, floating-point numbers, and complex numbers. 
- They can also be used with strings and lists, as well as other built-in data types that support the relevant operations.

## Comparison [[Python Operators]]

You can also compare numbers using comparison operators such as `<`, `>`, `<=`, `>=`, `==` (equality), and `!=` (not equal). For example:

```python
x = 5
y = 10
print(x < y)    # Output: True
print(x > y)    # Output: False
print(x <= y)   # Output: True
print(x => y)   # Output: False
print(x == y)   # Output: False
print(x != y)   # Output: True
```

## Built-in Functions

Python provides some built-in functions for working with numbers, such as `abs()`, `max()`, `min()`, `round()`, and `pow()`. For example:

```python
x = -4.7
y = 3.2
print(abs(x))   # Output: 4.7
print(max(x, y)) # Output: 3.2
print(min(x, y)) # Output: -4.7
print(round(x))  # Output: -5
print(round(y))  # Output: 3
print(pow(x, 2)) # Output: 22.09
```

---

## ~~[[Slicing]] of a Number~~

No, you **can not slice a number** in Python because numbers are considered as atomic data types, meaning they cannot be divided further into smaller elements. 

Slicing is a concept that applies to iterable objects like strings, lists, and tuples. 

However, you can convert a number to a string and then slice it. For example:

```python
num = 12345
str_num = str(num)
sliced_str_num = str_num[1:4]  # slice from index 1 to 4 (exclusive)
print(sliced_str_num)  # Output: "234"
```

---

## ~~[[Index]]of  a Number~~

No, **you can not index a number** in Python because numbers are considered as atomic data types, meaning they cannot be divided further into smaller elements. Indexing is a concept that applies to iterable objects like strings, lists, and tuples, where you can access individual elements by their position in the sequence using an index, ad esempio:

```python
num = 12345
str_num = str(num)
indexed_str_num = str_num[1]  # returns the character at the second index
print(indexed_str_num)  # Output: "2"
```

Note that after indexing the number as a string, the result will also be a string, not a number.

---
	
## ~~[[Loops]] in a Number~~

you can’t loop because a number is not iterable

---

## [[Modules]]

### Random Module

Python also has a `random` module for generating random numbers. For example:

```python
import random

print(random.randrange(1, 10)) # Output: a random integer between 1 and 9
print(random.random()) # Output: a random float between 0 and 1
```

### Math Module

For more advanced mathematical operations, Python has a `math` module. You can import the `math` module and use its functions, such as `sqrt()` for square roots and `sin()` for trigonometric sine. For example:

```python
import math

print(math.sqrt(16)) # Output: 4.0
print(math.sin(math.pi/2)) # Output: 1.0
```

---
