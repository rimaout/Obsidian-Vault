---
created: 2022-03-21
type: Programming Note
programming language: "[[Python MOC]]"
related: 
completed: true
updated: 2024-05-27T13:29
---
---
## Index 
1. [[#Introduction]]
2. [[#Line Comment]]
3. [[#Multiple Lines Comments]]

---
## Introduction 
Comments are parts of code that are not executed by the compiler

---
## Line Comment

Comments starts with a `#`, and Python will ignore them:
```Python
#This is a comment  
print("Hello, World!")
```

---
Comments can be placed at the end of a line, and Python will ignore the rest of the line:
``` Python
print("Hello, World!") #This is a comment
```

---
## Multiple Lines Comments
- Python does not really have a syntax for multiline comments.
- Since Python will ignore string literals that are not assigned to a variable, you can add a multiline string (triple quotes) in your code, and place your comment inside it:

```Python
"""  
This is a comment  
written in  
more than just one line  
"""  
print("Hello, World!")
```

---