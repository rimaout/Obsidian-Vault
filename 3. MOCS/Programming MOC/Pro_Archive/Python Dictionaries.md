---
created: 2023-03-03
type: Programming Note
programming language: "[[Python MOC]]"
related: 
completed: 
updated: 2024-05-27T13:29
---
---
# Dictionaries 
In Python, a dictionary is a collection of key-value pairs. It is an unordered, mutable, and indexed collection of elements. 
Dictionaries are also sometimes referred to as "maps", "hash maps", or "associative arrays" in other programming languages.

```python
my_dict = {"key1": "value1", "key2": "value2", "key3": "value3"}
```

The main characteristics of a list are:
1. **Defined  by curly braces {}**, and colons are used to separate keys and values.
3. **Iterable object:** can be divided in smaller parts, and you can use loops
4. **Mutable Object:** which means that can be modified
5. **[[Python Unordered Objects]]**: can't be sliced or indexed 
7. **Collection of element (values) associated to keys**

>[!warning] Nota:
> - ***keys*** can only be *immutable objects*, such as: integers, floats, strings, tuples
> - ***Values*** can be *any type of object*, such as integers, floats, strings, booleans, as well as more complex data types such as lists, tuples, and even other dictionaries.

Example:
```python
my_dict = {"name": "John", "age": 30, "is_student": True, "interests": ["reading", "sports"], "grades": {"math": 90, "science": 85}}
```

> [!warning] Key can't be repeated
>
---

## Concatenation and Replication 
[[Python Operators]]

**Concatenation Operator (+)**: This operator is used to concatenate two or more dictionaries into a one. For example:

```python

```

**Repetition Operator  ( * )** : This operator is used to repeat a dictionary a specified number of times. For example:

```python

```

---

### Comparison Operators


Here are some examples:

```python


```

---

## Built-in Functions

Python offers numerous built-in functions for working with lists. Here are some of the most commonly used functions:

### Getting a list length

#### len()

```python
>>> furniture = ['table', 'chair', 'rack', 'shelf']
>>> len(furniture)
# 4
```

### Adding Values

#### append()

`append` adds an element to the end of a `list`:

```python
>>> furniture = ['table', 'chair', 'rack', 'shelf']
>>> furniture.append('bed')
>>> furniture
# ['table', 'chair', 'rack', 'shelf', 'bed']
```

#### insert()

`insert` adds an element to a `list` at a given position:

```python
>>> furniture = ['table', 'chair', 'rack', 'shelf']
>>> furniture.insert(1, 'bed')
>>> furniture
# ['table', 'bed', 'chair', 'rack', 'shelf']
```

### Removing Values

#### del()

`del` removes an item using the index:

```python
>>> furniture = ['table', 'chair', 'rack', 'shelf']
>>> del furniture[2]
>>> furniture
# ['table', 'chair', 'shelf']

>>> del furniture[2]
>>> furniture
# ['table', 'chair']
```

#### remove()

`remove` removes an item with using actual value of it:

```python
>>> furniture = ['table', 'chair', 'rack', 'shelf']
>>> furniture.remove('chair')
>>> furniture
# ['table', 'rack', 'shelf']
```


>[!warning] Note:
>If the value appears multiple times in the list, only the first instance of the value will be removed.



#### pop()

By default, `pop` will remove and return the last item of the list. You can also pass the index of the element as an optional parameter:

```python
>>> animals = ['cat', 'bat', 'rat', 'elephant']

>>> animals.pop()
'elephant'

>>> animals
['cat', 'bat', 'rat']

>>> animals.pop(0)
'cat'

>>> animals
['bat', 'rat']
```

### Sorting values

#### sort()

```python
>>> numbers = [2, 5, 3.14, 1, -7]
>>> numbers.sort()
>>> numbers
# [-7, 1, 2, 3.14, 5]

furniture = ['table', 'chair', 'rack', 'shelf']
furniture.sort()
furniture
# ['chair', 'rack', 'shelf', 'table']
```

You can also pass `True` for the `reverse` keyword argument to have `sort()` sort the values in reverse order:

```python
>>> furniture.sort(reverse=True)
>>> furniture
# ['table', 'shelf', 'rack', 'chair']
```

If you need to sort the values in regular alphabetical order, pass `str.lower` for the key keyword argument in the sort() method call:

```python
>>> letters = ['a', 'z', 'A', 'Z']
>>> letters.sort(key=str.lower)
>>> letters
# ['a', 'A', 'z', 'Z']
```

You can use the built-in function `sorted` to return a new list:

```python
>>> furniture = ['table', 'chair', 'rack', 'shelf']
>>> sorted(furniture)
# ['chair', 'rack', 'shelf', 'table']
```

---

## [[Slicing]] of a List


>[!warning] Note:
Also, slicing a list does not modify the original list - it returns a new list that contains only the specified portion of the original list.

You can slice a list in Python using the same syntax `list[start:end:step]` as you would use for slicing a string, where:

- `start` is the index of the first element you want to include in the slice
- `end` is the index of the first element you want to exclude from the slice
- `step` is the number of elements to skip between each element included in the slice

Here are some examples:

```python
my_list = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# slice the entire list
print(my_list[:])           # Output: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# slice from index 0 to index 5 (excluding 5)
print(my_list[0:5])         # Output: [1, 2, 3, 4, 5]

# slice from index 7 to the end
print(my_list[7:])          # Output: [8, 9, 10]

# slice from index 2 to index 9, skipping every other element
print(my_list[2:9:2])       # Output: [3, 5, 7, 9]

# slice from the beginning to the end, skipping every other element
print(my_list[::2])         # Output: [1, 3, 5, 7, 9]

# slice from the end of the list to the beginning
print(my_list[::-1])        # Output: [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]

# slice from the end of the list to index 2 (excluding 2), skipping every other element
print(my_list[-1:1:-2])     # Output: [10, 8, 6, 4]

# slice from index -5 (5th element from the end) to index -1 (excluding -1), skipping every other element
print(my_list[-5:-1:2])     # Output: [6, 8]

# slice from index -8 (8th element from the end) to index -5 (excluding -5)
print(my_list[-8:-5])       # Output: [3, 4, 5]

# slice from index -3 (3rd element from the end) to the end of the list
print(my_list[-3:])         # Output: [8, 9, 10]

```

>[!warning] Note:
 >Like with strings, you can mix positive and negative indices in a single slice, and you can omit any of the three parameters (`start`, `end`, and `step`) as needed.
 
---

## [[Index]] of a List

In Python, a list is a collection  of elements, and you can access individual elements in the list by their position or index within the sequence.

- The index tarts at 0,
- The second character has an index of 1, and so on.

To access a specific element in a string, you can use its index within square brackets `[]`, like this:

```python
my_list = ["apple", "banana", "cherry"]
print(my_list[0])   # Output: "apple"
print(my_list[1])   # Output: "banana"
print(my_list[2])   # Output: "cherry"
```


>[!warning] Note:
The index must be an integer, and it must be within the range of valid indices for the string (from 0 to `len(lits) - 1`).  Otherwise, a `IndexError` will be raised.

You can also use **negative indices** to access elements from the end of the list:

```python
my_list = ["apple", "banana", "cherry"]
print(my_list[-1])   # Output: "cherry"
print(my_list[-2])   # Output: "banana"
print(my_list[-3])   # Output: "apple"
```

To find the index of a particular element in a list, you can use the **index() method**, just like with strings:

```python
my_list = ["apple", "banana", "cherry"]
element = "banana"
index = my_list.index(element)
print(index)   # Output: 1
```

In this example, we define a list `my_list` and an element `element`, and then use the `index()` method to find the index of the first occurrence of `element` within `my_list`. The result is 1, which is the index of the second element in the list.


>[!warning] Note:
If the element `element` is not found in the list, a `ValueError` will be raised.

### Modify an element using the index

you can also use the index operator `[]` to modify an element in a list. Here's an example:

```python
my_list = ["apple", "banana", "cherry"]
my_list[1] = "orange"
print(my_list)   # Output: ["apple", "orange", "cherry"]
```

---

## [[Loops]] in a List

In Python, a loop is a programming construct that allows you to iterate over a sequence of items, such as the characters in a string.

There are two types of loops in Python: the `for` loop and the `while` loop.

- we use a `for` loop to iterate over each character in the string.
    
    ```python
    string = "hello"
    for char in string:
        print(char)
    ```
    

In Python, you can use loops to iterate over the elements in a list. There are two main types of loops you can use: `for` loops and `while` loops.

### For Loops

- we use a `for` loop to iterate over each element in the list
    
    ```python
    my_list = [1, 2, 3, 4, 5]
    for element in my_list:
        print(element)
    
    # This code will output alle the elements inside the list
    ```
    
    - You can also use the `range()` function to iterate over a range of indices in the list:
        
        ```python
        my_list = [1, 2, 3, 4, 5]
        for i in range(len(2)):
            print(my_list[i])
        
        # This code will output the first 3 elemets (from o to 2)
        ```
        

### While Loops

- `while` loop is designed to repeat a block of code while a specific condition is true
    
    ```python
    my_list = [1, 2, 3, 4, 5]
    index = 0
    while index < len(my_list):
        print(my_list[index])
        index += 1
    ```

---