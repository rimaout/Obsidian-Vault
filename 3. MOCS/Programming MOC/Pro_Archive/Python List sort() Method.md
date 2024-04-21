---
Created: 2024-07-14
Type: Programming Note
Programming Language: "[[Python MOC]]"
Related:
  - "[[Python sorted() Function]]"
  - "[[Sorting Algorithms]]"
  - "[[Python Functions - Methods]]"
Completed: true
---
---
# Index
1. [[Python List sort() Method#Definition|Definition ]]
2. [[Python List sort() Method#Syntax|Syntax]]
3. [[Python List sort() Method#Parameter Values|Parameter Values]]
4. [[Python List sort() Method#Return Values|Return Values]]
5. [[Python List sort() Method#key Parameter in Python sort()|Key Parameter]]

---
## Definition 
The `sort()` method sorts the items of a [[Python Lists|list]] in ascending or descending order.

---
## Syntax

The syntax of the `sort()` method is:

```python
list.sort(key=..., reverse=...)
```

Alternatively, you can also use built-in [[Python sorted() Function]] for the same purpose.

>[!Note:] 
>The simplest difference between `sort()` and `sorted()` is: `sort()` changes the list directly and doesn't return any value, while `sorted()` doesn't change the list and returns the sorted list.

---
## Parameter Values

|Parameter|Description|
|---|---|
|*iterable*| Iterator objects that will be joined together |
|*reverse (Optional)*|If `True`, the sorted list is reversed (or sorted in descending order). Defaults to `False` if not provided.|
|*key (Optional)* | A function that serves as a key for the sort comparison. Defaults to `None`. |

---
## Return Values

- The `sort()` method doesn't return any value. Rather, it changes the original list.

- If you want a function to return the sorted list rather than change the original list, use `sorted()`.

**Example 1) Sort a given list:

```python
# vowels list
vowels = ['e', 'a', 'u', 'o', 'i']

# sort the vowels
vowels.sort()

# print vowels
print('Sorted list:', vowels)
# Output: Sorted list: ['a', 'e', 'i', 'o', 'u']
```

**Example 2) Sort in Descending order:

Setting `reverse = True` sorts the list in the descending order.

```python
# vowels list
vowels = ['e', 'a', 'u', 'o', 'i']

# sort the vowels
vowels.sort(reverse=True)

# print vowels
print('Sorted list (in Descending):', vowels)
# Output: Sorted list (in Descending): ['u', 'o', 'i', 'e', 'a']
```

---
## key Parameter in Python sort()

If you want your own implementation for sorting, the `sort()` method also accepts a `key` function as an optional parameter.
**Example using len() function has a key parameter:**
- Here, `len` is Python's in-built function to count the length of an element.
- The list is sorted based on the length of each element, from lowest count to highest.

```python


# String list
lista = ["ciao", "straordinario", "mondo"]

# sort list with key
lista.sort(key=len)

# print list
print(lista)
# Output:['ciao', 'mondo', 'straordinario']
```

---
## Particular examples 
**Read:** [[Python sorted() Function#Examples]] to see more interesting and powerful examples

---