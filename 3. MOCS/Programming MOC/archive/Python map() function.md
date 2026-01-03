---
created: 2023-11-16
type: Programming Note
programming language: "[[Python MOC]]"
related:
  - "[[Python Functions - Methods]]"
completed: true
updated: 2024-05-27T13:29
---
---
## Index
1. [[#Definition]]
2. [[#Syntax]]
3. [[#Parameter Values (input)]]
4. [[#Return Values (output)]]

---
## Definition
**map()** function returns a map object(which is an *iterator*) of the results after applying the given function to each item of a given iterable (list, tuple etc.)

>[!warning] oss: 
>if you what to print the result of map  you have to translate i to a list or tuple or set (ex: list(map) ,set(map) ...) 
>- this because map returns the address of map object [[Python How to print a object|example]]

---
## Syntax
```python
map(fun, *iterables)
```

> [!Parameter Values (input):]
>- *fun:* - It is a function to which map passes each element of given iterable.
>- *iterables:* It is iterable which is to be mapped.
> 
>	**NOTE:** You can pass one or more iterable to the map() function.



> [!Return Values (output):] 
> - Returns a list of the results after applying the given function to each item of a given iterable (list, tuple etc.)

---
## Example

**One Iterator:**
``` python
def double(n):
    return n*2

numbers = (1, 2, 3, 4)

list(map(double, numbers)) #Output: [2, 4, 6, 8]
```

*labda version:*
```python
numbers = (1, 2, 3, 4)

list(map(lambda x: x*2, numbers)) #Output: [2, 4, 6, 8]
```

> [!nota] Why list(map(...))
> because if you print(map) without the list you will print 


**Two Iterator:**
``` python
numbers1 = [1, 2, 3]
numbers2 = [4, 5, 6]

list(map(lambda x, y: x + y, numbers1, numbers2))  #Output: [5, 7, 9]
```

**Advanced Two Iterators:**
``` python
def upper_lower(inter1, iter2):
	return iter1.apper(), iter2.lower()


list(map(upper_lower, ["jAx", "KeEpEr"], ["ToNy", "sTaRk"]))
#Output: [("JAX", "keper"), ("TONY", "stark")]
```

*labda version:*
```python
list(map(lambda x,y: (x.upper(),y.lower()),  ["jAx", "KeEpEr"], ["ToNy", "sTaRk"]))
#Output: [('JAX', 'tony'), ('KEEPER', 'stark')]
```

---