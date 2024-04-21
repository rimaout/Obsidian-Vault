---
Created: 2023-09-24
Type: Programming Note
Programming Language: "[[Python MOC]]"
Related: "[[Python Print Parameters]]"
Completed: true
---
---
# Index
1. [[#Introduction]]
2. [[#Common Escape Sequences in Python]]
3. [[#Examples]]
4. [[#Raw Strings]]

---
## Introduction
An escape sequence is a special character used in the form of **backslash(\)** followed by a **character** that is required. These characters are used to represent whitespace. Whitespace gives characters like space, tab, form-feed, and vertical tab.

---
## Common Escape Sequences in Python
|Escape Sequence|Description|
|---|---|
|`\\`|Backslash (`\`)|
|`\'`|Single quote (`'`)|
|`\"`|Double quote (`"`)|
|`\n`|Newline|
|`\t`|Tab|
|`\r`|Carriage return|
|`\b`|Backspace|
|`\f`|Form feed|
|`\ooo`|Character with octal value ooo|
|`\xhh`|Character with hex value hh|

---
## Examples

**New line:**
```python
print("ciao\n mamma")

# Output: ciao
#         mamma
```

**Backslash:**
```python
print("ciao\\ mamma")

# Output: ciao\ mamma
```

**Space:**
```python
print("ciao\tmamma")

# Output: ciao mamma
```

**Backspace:** 
```python
print("ciao \bmamma")

# Output: ciaomamma
```
*oss:* remove's the space between to words

**Hexa value:**
```python
print("```
\x50\x59\x54\x48\x4f\x4E \x47\x55\x49\x44\x45\x53
```")

# Output: PYTHON GUIDES
```
*oss:* it's used to convert hexa value into a string

**Octal value:**
```python
print("```
\120\131\124\110\117\116 \107\125\111\104\105\123
```")

# Output: PYTHON GUIDeS
```

---
## Raw Strings
In Python, you can create raw strings by prefixing the string with the letter r or R. In raw strings, backslashes are treated as literal characters and not as escape characters in Python.

``` python
raw_string = r"This is a raw string\nThis will not be on a new line"

print(raw_string)

```

---