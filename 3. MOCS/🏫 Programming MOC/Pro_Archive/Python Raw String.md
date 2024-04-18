---
Created: 2023-09-29
Type: Programming Note
Programming Language: "[[Python MOC]]"
Related:
  - "[[Python Strings]]"
  - "[[Python Backslash (escaping character)]]"
  - "[[Python Escaping Sequences]]"
Completed: true
---

**read:** [[Python Backslash (escaping character)]] and [[Python Escaping Sequences]]

---
## Definition

In Python, when you prefix a string with the letter `r` or `R` such as `r'...'` and `R'...'`, that string becomes a raw string. Unlike a regular string, a raw string treats the backslashes (`\`) as literal characters.

Raw strings are useful when you deal with strings that have many backslashes, for example directory paths on Windows.

**Example:**
```python
s = "lang\tver\nPython\t3 print(s)"
```
Output:
```
Output:

lang    ver 
Python  3
```

However, raw strings treat the backslash (`\`) as a literal character. For example:
```python
s = r"lang\tver\nPython\t3"

print(s) #Output: lang\tver\nPython\t3
```

---
##  Convert a regular string into a raw string

To convert a regular string into a raw string, you use the built-in repr() function. For example:

```python
s = '\n'
raw_string = repr(s)

print(raw_string) #Output: \n
```

---