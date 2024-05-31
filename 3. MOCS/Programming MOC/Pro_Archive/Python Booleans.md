---
created: 2022-03-18
type: Programming Note
programming language: "[[Python MOC]]"
related: 
completed: true
updated: 2024-05-27T13:29
---
---
## Index
1. [[#Definition]]
2. [[#Evaluate Values and Variables]]
3. [[#Python Comparison Operators Comparison operators return Boolean values|Comparison operators return Boolean values]]
4. [[#Python Functions - Methods Functions can Return a Boolean|Functions can Return a Boolean]]

---
## Definition 
In programming you often need to know if an expression is `True` or `False`

## Evaluate Values and Variables
You can evaluate any expression in Python, and get one of two answers, `True` or `False.

 - The `bool()` function allows you to evaluate any value, and give you `True` or `False` in return,
 
When you compare two values, the expression is evaluated and Python returns the Boolean answer:
```python
print(bool("Hello"))  # Output: True
print(bool(15))       # Output: True
```

**Most Values are True**
- Almost any value is evaluated to `True` if it has some sort of content.
	- Any string is `True`, except empty strings.
	- Any number is `True`, except `0`.
	- Any list, tuple, set, and dictionary are `True`, except empty ones.

**Some Values are False**
- In fact, there are not many values that evaluate to `False`, except empty values, such as `()`, `[]`, `{}`, `""`, the number `0`, and the value `None`. And of course the value `False` evaluates to `False`.
```python 
bool(False)  # Output: False
bool(None)   # Output: False
bool(0)      # Output: False
bool("")     # Output: False
bool(())     # Output: False
bool([])     # Output: False
bool({}).    # Output: False
```

---
## [[Python Comparison Operators|Comparison operators]] return Boolean values
When you compare two values, the expression is evaluated and Python returns the Boolean answer:
```python 
print(10 > 9)   # Output: True
print(10 == 9)  # Output: False
print(10 < 9)   # Output: False
```

**Particular cases:**
```python
print(1 == True)   #Output: True
print(0 == False)  #Output: True
print(1 == 1.0000) #Output: True
```

---
## [[Python Functions - Methods|Functions]] can Return a Boolean
You can create functions that returns a Boolean Value:
```python 
def myFunction() :  
  return True  
  
if myFunction():  
  print("YES!")  
else:  
  print("NO!")
```

Python also has many built-in functions that return a boolean value, like the `isinstance()` function, which can be used to determine if an object is of a certain data type:
```python 
x = 200  
print(isinstance(x, int))
```

---