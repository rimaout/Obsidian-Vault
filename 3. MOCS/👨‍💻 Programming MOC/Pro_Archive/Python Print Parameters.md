---
Created: 2023-09-24
Type: Programming Note
Programming Language: "[[Python MOC]]"
Related:
  - "[[Python Print()]]"
Completed: true
---
---
# Index
1. [[#Introduction]]
2. [[#End Parameters]]
3. [[#Sep Parameters]]

---
## Introduction
The print function has some parameters that let you interact with the output of the function

---
## End Parameters
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
## Sep Parameters
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
## File parameter
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