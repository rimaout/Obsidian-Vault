---
created: 2023-07-14
type: Programming Note
programming language: "[[Python MOC]]"
related:
  - "[[Sorting Algorithms]]"
  - "[[Python Functions - Methods]]"
completed: true
updated: 2024-05-27T13:29
---
---
# Index
1. [[#Definition]]
2. [[#Syntax]]
3. [[#Parameter Values (input)]]
4. [[#Return Values]]
5. [[#key Parameter in Python sorted() function]]
6. [[#Examples:]]
	- [[#Sorting a dict by the values]]
	- [[#Sorting agenda by specific info]]

---
## Definition 
The `sorted()` function sorts the elements of a given [[Python Iterators, __iter__ and __next__|iterable]] in a specific order (ascending or descending) and returns it as a list.

---
## Syntax
```python
sorted(iterable, key=None, reverse=False)
```

---
## Parameter Values (input)

|Parameter|Description|
|---|---|
|*iterable*| Iterator objects that will be joined together |
|*reverse (Optional)*|If `True`, the sorted list is reversed (or sorted in descending order). Defaults to `False` if not provided.|
|*key (Optional)* | A function that serves as a key for the sort comparison. Defaults to `None`. |

**Recommended Reading:** [[Python Iterators, __iter__ and __next__]]

---
## Return Values

>[!warning] oss:
> - `sorted()` returns always a list independently of the input type

**Example 1) Sort string, list, and tuple;**
```python
# vowels list
py_list = ['e', 'a', 'u', 'o', 'i']
print(sorted(py_list)) 
# Output: ['a', 'e', 'i', 'o', 'u']

# string
py_string = 'Python'
print(sorted(py_string)) 
# Output: ['P', 'h', 'n', 'o', 't', 'y']


# vowels tuple
py_tuple = ('e', 'a', 'u', 'o', 'i') 
# Output: ['a', 'e', 'i', 'o', 'u']

print(sorted(py_tuple))
```

**Example 2) Sort in descending order:**

The `sorted()` function accepts a `reverse` parameter as an optional argument.

Setting `reverse = True` sorts the iterable in the descending order.
```python
# set
py_set = {'e', 'a', 'u', 'o', 'i'}
print(sorted(py_set, reverse=True))
# Output: ['u', 'o', 'i', 'e', 'a']

# dictionary
py_dict = {'e': 1, 'a': 2, 'u': 3, 'o': 4, 'i': 5}
print(sorted(py_dict, reverse=True))
# Output: ['u', 'o', 'i', 'e', 'a']

# frozen set
frozen_set = frozenset(('e', 'a', 'u', 'o', 'i'))
print(sorted(frozen_set, reverse=True))
# Output: ['u', 'o', 'i', 'e', 'a']
```

---
## Key Parameter in Python sorted() function

If you want your own implementation for sorting, `sorted()` also accepts a `key` function as an optional parameter.

Based on the returned value of the key function, you can sort the given iterable.

**Example 1:**
```python
sorted(iterable, key=len)
```
Here, `len()` is Python's in-built function to count the length of an object.
The list is sorted based on the length of the element, from the lowest count to highest.

**Example2:**
``` python
# take the second element for sort
def take_second(elem):
    return elem[1]


# random list
random = [(2, 2), (3, 4), (4, 1), (1, 3)]

# sort list with key
sorted_list = sorted(random, key=take_second)

# print list
print('Sorted list:', sorted_list)
# Output: Sorted list: [(4, 1), (2, 2), (1, 3), (3, 4)]
```

---
## Examples:

### Sorting a dict by the values
**oss:** Usually a dict i sorted by the key 

```python
py_dict = {'a': 5, 'e': 4, 'i': 3, 'o': 2, 'u': 1}
print(sorted(py_dict, key = lambda x: py_dict.get(x)))
# Output: ['u', 'o', 'i', 'e', 'a']
```

### Sorting agenda by specific info

``` python
agenda =[ 
		  {'nome':'Paperino','cognome':'Paolino', 'phone':'555-1313', 'city':'Paperopoli'},
		  {'nome':'Gastone', 'cognome':'Paperone', 'telefono':'555-1717', 'città':'Paperopoli'},
		  {'nome': 'Archimede','cognome':'Pitagorico','telefono':'555-11235', 'città': 'Paperopoli'}
		]

print(agenda_sorted = sorted(agenda, key=lambda diz: (diz['cognome'])))

#Output: [{'nome': 'Paperino', 'cognome': 'Paolino', 'phone': '555-1313', 'city': 'Paperopoli'}, 
#         {'nome': 'Gastone', 'cognome': 'Paperone', 'telefono': '555-1717', 'città': 'Paperopoli'}, 
#         {'nome': 'Archimede', 'cognome': 'Pitagorico', 'telefono': '555-11235', 'città': 'Paperopoli'}]

```


---