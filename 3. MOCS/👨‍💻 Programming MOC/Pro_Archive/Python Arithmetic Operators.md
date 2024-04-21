---
Created: 2023-05-04
Type: Programming Note
Programming Language: "[[Python MOC]]"
Related: 
Completed:
---
---
## Index
1. [[#Introduction]]
2. [[#Arithmetic operators and Python Numbers]]
3. [[#Arithmetic operators and Python Strings]]
4. [[#Arithmetic operators and Python Lists]]
5. [[#Arithmetic operators and Python Tuples]]
6. [[#Arithmetic operators and Python Dictionaries]]

---
## Introduction

|Operator|Name|Example|
|---|---|---|
|+|Addition|x + y|
|-|Subtraction|x - y|
|\*|Multiplication| x \* y|
|/|Division|x / y|
|%|Modulus|x % y|
|\*\*|Exponentiation|x \*\* y|
|//|Floor division|x // y|

***scrivi precedenze operatori***

---
## Arithmetic operators and [[Python Numbers]]

``` python
a = 7
b = 2

# addition
print ('Sum: ', a + b)    # Output: 9

# subtraction
print ('Subtraction: ', a - b)     # Output: 5

# multiplication
print ('Multiplication: ', a * b)    # Output: 14

# division
print ('Division: ', a / b)    # Output: 3.5

# floor division
print ('Floor Division: ', a // b)    # Output: 3

# modulo
print ('Modulo: ', a % b)    # Output: 1

# a to the power b
print ('Power: ', a ** b)    # Output: 49
```
 
 **oss:** when doing a operation between a integer ad a floating point the end result will be always a floating point
 ```python
x = 2 + 1.00
print(x) #Output: 3.00000
```

---
## Arithmetic operators and [[Python Strings]]

**2 Strings:**
``` python
a = "hello"
b = "word"

# addition
print ('Sum: ', a + b)    # Output: 9

# subtraction
print ('Subtraction: ', a - b)     # Output: ERROR

# multiplication
print ('Multiplication: ', a * b)    # Output: ERROR

# division
print ('Division: ', a / b)    # Output: ERROR

# floor division
print ('Floor Division: ', a // b)    # Output: ERROR

# modulo
print ('Modulo: ', a % b)    # Output: ERROR

# a to the power b
print ('Power: ', a ** b)    # Output: ERROR
```

**Strings and a number:**
``` python
a = "hello"
b = "2"

# addition
print ('Sum: ', a + b)    # Output: ERROR

# subtraction
print ('Subtraction: ', a - b)     # Output: ERROR

# multiplication
print ('Multiplication: ', a * b)    # Output: hellohello

# division
print ('Division: ', a / b)    # Output: ERROR

# floor division
print ('Floor Division: ', a // b)    # Output: ERROR

# modulo
print ('Modulo: ', a % b)    # Output: ERROR

# a to the power b
print ('Power: ', a ** b)    # Output: ERROR
```

>[!danger] oss:
>- A sting is an [[Python Data Types#Mutable and unmutable datatypes|unmutable datatype]], this means that can't be modified
> - For this reason every time that we do a arithmetic operation on a string we are not modifying it but we are generating a new one

---
## Arithmetic operators and [[Python Lists]]


---
## Arithmetic operators and [[Python Tuples]]


---
## Arithmetic operators and [[Python Dictionaries]]


---
## Arithmetic operators and [[Python Sets]]


---