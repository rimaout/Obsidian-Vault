---
created: 2023-03-03
type: Programming Note
programming language: "[[Python MOC]]"
related: 
completed: true
updated: 2024-10-03T16:19
---
---
# Tuple

```python
my_tuple = (1, "hello", True)
```

The main characteristics of a tuple are:

1. **Defined  by  round bracts**, and each element in the tuple is separated by a comma
2. **Collection fo elements** that can be of any data type
3. **Iterable object:** can be divided in smaller parts 
4. **Immutable Object:** which means that can not be modified
5. **Orderd:** ammit the repetiton of elements and can be sliced and indexed
    
>[!question] Why use tuples?
>If an array is not to be changed, it is preferable to use a tuple rather than a list for the following reasons:
> - **The computation is faster**. Processing time for a tuple is less than for a list.
     > - **Memory space is less**. Tuples consume less memory space than lists.

>[!warning] The sintax for a one-element tuple is:
>> - `tuple = (x, )`
---

## Concatenation and Replication
[[Python Operators]]
>[!note:]
>Work's in the same way of lits
> - read: [[Python Lists#**Concatenation and Replication**]] to know more
---

### Comparison Operators

[[Python Operators]]
>[!note:]
>Work's in the same way of lits
> - read: [[Python Lists#**Comparison Operators**]] to know more
---

## Built-in Functions
Tuples are immutable data structures in Python, and they provide a convenient way to group related data together. Here are the 10 most commonly used tuple functions in Python:

1. **len()**: Returns the length of a tuple.
```python
t = (1, 2, 3, 4, 5)
print(len(t)) # Output: 5

```

2. **tuple()**: Creates a new tuple from a sequence or iterable.
```python
s = "hello"
t = tuple(s)
print(t) # Output: ('h', 'e', 'l', 'l', 'o')
```

3. **count()**: Returns the number of occurrences of a value in a tuple.
```python
t = (1, 2, 2, 3, 3, 3, 4, 5)
print(t.count(3)) # Output: 3
```

4.  **index()**: Returns the index of the first occurrence of a value in a tuple.
```python
t = (1, 2, 3, 4, 5)
print(t.index(3)) # Output: 2
```

5. **sorted()**: Returns a new sorted list from a tuple.
```python
t = (5, 3, 1, 2, 4)
sorted_t = sorted(t)
print(sorted_t) # Output: [1, 2, 3, 4, 5]
```

6.  **max()**: Returns the maximum value in a tuple.
```python
t = (1, 2, 3, 4, 5)
print(max(t)) # Output: 5
```

7.  **min()**: Returns the minimum value in a tuple.
```python
t = (1, 2, 3, 4, 5)
print(min(t)) # Output: 1
```

8.  **any()**: Returns `True` if any element in the tuple is `True`, otherwise `False`.
```python
t = (False, 0, "", 4)
print(any(t)) # Output: True
```

9.  **all()**: Returns `True` if all elements in the tuple are `True`, otherwise `False`.
```python
t = (True, 1, "hello")
print(all(t)) # Output: True
```

10. **enumerate()**: Returns an iterable of tuples, where each tuple contains the index and value of each element in the original tuple
```python
t = ("apple", "banana", "cherry")
for index, value in enumerate(t):
    print(index, value)

# Output:
# 0 apple
# 1 banana
# 2 cherry
```
---

## [[Slicing]] of a List
>[!note:]
>Work's in the same way of lists
> - read: [[Python Lists#** Slicing of a List**]] to know more

---
## [[Quartz Index Example]]of a List
>[!note:]
>Work's in the same way of lists
> - read: [[Python Lists#** Index of a List**]] to know more

>[!warning ] Difference:
>There is a main difference between lists and tuples, tuples are immutable.
>- `tuple = (1,2,3,4)`
>- `tuple[0] = 5` ---> is impossible, you can't change an elemet of a tuple

---
## [[Loops]] in a List
>[!note:]
>Work's in the same way of lists
> - read: [[Python Lists#** Loops in a List**]] to know more

---
## [[Python Conversion Between Tupels and Lists]]
