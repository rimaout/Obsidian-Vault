Completed: Yes
Created: March 2, 2023
Tag: [[Python MOC]]

---
## List To Tuple

**tuple()** Funcion:
In Python, a tuple is an ordered collection of values that can be of any data type. The `tuple()` function is used to create a tuple object from a sequence or iterable.

The syntax for using the `tuple()` function is as follows:

```python
tuple(iterable)
```

Here, `iterable` is any sequence such as a list, string, or range object that you want to convert to a tuple. The `tuple()` function takes the iterable object and converts it into a tuple object.

For example, consider the following code:

```python
lst = [1, 2, 3]
tpl = tuple(lst)
print(tpl)

# Output: (1, 2, 3)
```

You can also use the `tuple()` function to create an empty tuple. For example:

```python
tpl = tuple()
print(tpl)

# Output: ()
```


## Tupel to Lists

**list()** Funcion:
In Python, a list is an ordered collection of values that can be of any data type. The `list()` function is used to create a list object from a sequence or iterable.

The syntax for using the `list()` function is as follows:

```python
list(iterable)
```

Here, `iterable` is any sequence such as a tuple, string, or range object that you want to convert to a list. The `list()` function takes the iterable object and converts it into a list object.

For example, consider the following code:

```python
tpl = (1, 2, 3)
lst = list(tpl)
print(lst)

# Output: [1, 2, 3]
```

You can also use the `list()` function to create an empty list. For example:

```python
lst = list()
print(lst)

# Output: []
```