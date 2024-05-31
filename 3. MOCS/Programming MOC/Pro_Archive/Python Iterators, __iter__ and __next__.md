---
created: 2023-03-21
type: Programming Note
programming language: "[[Python MOC]]"
related: 
completed: 
updated: 2024-05-27T13:29
---
---
## Index
1. [[#Definition]]
2.  [[#_ _iter _ _()]]
3.  [[#_ _next _ _()]]
4. [[#Building Custom Iterators]]

---
## Definition
- Iterators are methods that can be used on [[iterable objects]] 
- Using an iterator method, we can loop through an object and return its elements.

Technically, a Python **iterator object** must implement two special methods, `__iter__()` and `__next__()`, collectively called the **iterator protocol**.

---
## \_\_iter\_\_()

In Python, we can use the `iter()` function to create an iterator.
``` python
# create a list of integers
my_list = [1, 2, 3, 4, 5]

# create an iterator from the list
iterator = iter(my_list)
```

---
## \_\_next\_\_()

In Python, we can use the `next()` function to return the next item in the sequence.

```python
# define a list
my_list = [4, 7, 0]

# create an iterator from the list
iterator = iter(my_list)

# get the first element of the iterator
print(next(iterator))  # prints 4

# get the second element of the iterator
print(next(iterator))  # prints 7

# get the third element of the iterator
print(next(iterator))  # prints 0
```

---
## Building Custom Iterators


---
