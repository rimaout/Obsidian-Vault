---
created: 2023-09-29
type: Programming Note
programming language: "[[Python MOC]]"
related:
  - "[[Python f-string]]"
completed: true
updated: 2024-05-27T13:29
---
---
## Index
1. [[#Introduction]]
2. [[#Syntax]]
3. [[#All the different ways of printing a string]]
4. [[#f-string]]
5. [[#Print parameters]]
	1. [[#End Parameters (optional)]]
	2. [[#Sep Parameters (optional)]]
	3. [[#File (optional)]] 
	1. [[#Flush parameter (optional)]]

---
## Introduction
The `print()` function prints the specified message to the screen, or other standard output device.

The message can be a string, or any other object, the object will be converted into a string before written to the screen.

---
## Syntax
```
print(*args, sep=' ', end='\n', file=None, flush=False)
```

**Brackets use:**
if you want to print a string directly from the print function you can open a string with:
- **"** : doing so you can use *'* without closing the string
- **'** : doing so you can use *"* without closing the string
```python
print("I'm Matteo's computer") 
print('The computer said: "I am the computer of Matteo"')
```

**\*args use:**
you can print all the element in a iterable object 
```python
L = ["Ciao", "Hello", "Hola"]
print(L)   #Output: ["Ciao", "Hello", "Hola"]
print(*L)  #Output: Ciao Hello Hola

#OSS: its the same thing of a for
#    for e in L:
#        print(e, end='')   #Output: Ciao Hello Hola
```

---
# All the different ways of printing a string 

```python
name = "Matteo"
age = 20

print(f" I'm {name} and i'm {age} years old")
print("I'm   and i'm {} years old", name, age)
print("I'm " + str(name) +  " and i'm " + str(age) + "years old")
print("I'm ", name, "and i'm", age, "years old")
```

---
## f-string

f-strings allow you to easily incorporate Python expressions into strings using the syntax `{expression}`.

Here are some examples of f-strings in Python:
```python
name = "Mario"
age = 30

# incorporate variables into a string
print(f"My name is {name} and I'm {age} years old.")

# evaluate expressions within a string
print(f"{name.upper()} is shouting!")

# incorporate formatted values into a string
num = 42
print(f"The answer to everything is {num:03d}")
```

**oss:** Using f-strings let you print print data types different form a sting without converting them
```python
print(f" I'm {name} and i'm {age} years old")
print("I'm " + str(name) +  " and i'm " + str(age) + "years old")
```

---
## Print parameters 
The print function has some parameters that let you interact with the output of the function

---
### End Parameters (optional)
The end parameter decide witch character goes at the end of the print

***By default*** Python‘s print() function ends with a *newline*
``` python
print("Welcome to")
print("Europe")

# Output: Welcome to
#         Europe
```

But it can be changed with every string or [[Python Escaping Sequences]]
```python
print("Welcome to", end=' ')
print("Europe")

# Output: Welcome to Europe

```

---
### Sep Parameters (optional)
The step parameter decide witch character separates 2 o more objects, ***by default*** its a space symbol (*" "*)
```python
a = 5
b = 5

print(a, b) #Output: 5 5
```

but it can be change with every string or [[Python Escaping Sequences]]
```python

a = 5
b = 5

print(a, b, sep = "=") #Output: 5=5
```

---
### File  (optional)
In Python, you can print objects to the file by specifying the file parameter.

***By default*** is set as `sys.stdout` which prints objects on the screen

But it can be change with every file thats open in writing mode
```python
sourceFile = open('python.txt', 'w')
print('1', file = sourceFile)
print('2', file = sourceFile)
print('3', file = sourceFile)
sourceFile.close()

```

```
file content:
--------------------------
1
2
3
--------------------------
```

This program in particular tries to open python.txt, but if it doesn't exist in the directory that you are working in it will be created 

**oss:** every time you open the file in this way all the text inside the file will be cleared

**Read [[Python Files]] to learn more**

---
### Flush parameter (optional)


- *Boolean value*, specifying if the output is flushed (True) or buffered (False). 
- *ByDefault* is False|