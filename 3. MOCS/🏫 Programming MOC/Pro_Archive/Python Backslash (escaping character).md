---
Created: 2023-09-28
Type: Programming Note
Programming Language: "[[Python MOC]]"
Related:
  - "[[Python Escaping Sequences]]"
Completed: true
---
# Index
1. [[#Intro]]
2. [[#Uses cases]]
3. [[#Backslash in F-strings]]
4. [[#Raw Strings]]

---
# Intro

In Python, the backslash(`\`) is a special character. If you use the backslash in front of another character, it changes the meaning of that character.

---
# Uses cases
- Use the Python backslash (`\`) to escape other special characters in a string.
**Example:** if you have a string that has a single quote inside a single-quoted string like the following string, you need to use the backslash to escape the single quote character:
```python
s = '"Python\'s awesome" She said'
```

- it's used in the [[Python Escaping Sequences]] to ad more functionality to the [[Python Strings]].

---
# Backslash in F-strings

>[!warning]
>that an [[Python Strings#f-string]] cannot contain a backslash character as a part of the expression inside the curly braces `{}`.

```python
colors = ['red','green','blue'] 
s = f'The RGB colors are:\n {'\n'.join(colors)}' print(s)
```
Output:
```python
SyntaxError: f-string expression part cannot include a backslash
```

---

# Raw Strings
![[Python Strings#raw-string]]