---
Created: 2023-06-14
Programming Language: "[[Python MOC]]"
Related: 
Completed:
---
---
## Index
-  [[#Zip]]:
		1. [[#Definition]]
		2. [[#Syntax]]
		3. [[#Parameter Values]]
		4. [[#Return Values]]

-  [[#UnZipping]]:

---
# Zip
## Definition 
The `zip()` function returns a zip object, which is an iterator of **tuples** where the first item in each passed iterator is paired together, and then the second item in each passed iterator are paired together etc.

If the passed iterators have different lengths, the iterator with the least items decides the length of the new iterator.

---
## Syntax
`zip(iterator1, iterator2, iterator3 ...)`

---
## Parameter Values

|Parameter|Description|
|---|---|
|_iterator1, iterator2, iterator3 ..._| Iterator objects that will be joined together |

**oss:** can be built-in iterables (like: list, string, dict), or user-defined iterables

**Recommended Reading:** [[Python Iterators, __iter__ and __next__]]

---
## Return Values

The `zip()` function returns an iterator of **tuples** based on the iterable objects.

1.  If we do not pass any parameter, `zip()` returns an empty iterator
2.  If a single iterable is passed, `zip()` returns an iterator of tuples with each tuple having only one element.
3.  If multiple iterables are passed, `zip()` returns an iterator of tuples with each tuple having elements from all the iterables.  
      
    Suppose, two iterables are passed to `zip()`; one iterable containing three and other containing five elements. Then, the returned iterator will contain three tuples. It's because the iterator stops when the shortest iterable is exhausted.

**Examples no parameters:**
```python
result = (zip())

# oss: use a list/tuple funcione too make the zip object readable
print(tuple(result))
# Output: ()
```

**Examples one parameters:**
```python
list = [1, 2, 3, 4]
result = (zip(list))

# oss: use a list/tuple funcione too make the zip object readable
print(list(result))
# Output: [(1,), (2,), (3,), (4,)]
```

**Examples multiple parameters (same length):** 
```python
languages = ['Java', 'Python', 'JavaScript']
versions = [14, 3, 6]

result = zip(languages, versions)

print(list(result))
# Output: [('Java', 14), ('Python', 3), ('JavaScript', 6)]
```

**Examples multiple parameters (different length):**
```python
languages = ['Java', 'Python', 'JavaScript']
versions = [14, 3, 6]
difficulty = [1000]

result = zip(languages, versions, difficulty)

print(list(result))
# Output: [('Java', 14, 100)]
```

---
## UnZipping

```python
coordinate = ['x', 'y', 'z']
value = [3, 4, 5]

result = zip(coordinate, value)
result_list = list(result)
print(result_list)

c, v =  zip(*result_list)
print('c =', c)
print('v =', v)
```

**Output:**
```
[('x', 3), ('y', 4), ('z', 5)]
c = ('x', 'y', 'z')
v = (3, 4, 5)
```

---