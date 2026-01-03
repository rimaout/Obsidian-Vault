---
created: 2023-03-30
type: Programming Note
programming language: "[[Python MOC]]"
related: 
completed: true
updated: 2024-05-27T13:29
---
---
- C uses `char` type to store characters and letters. 
- However, the `char` type is [integer type](C%20Numbers.md) because underneath C stores integer numbers instead of characters.

To represent characters, the computer has to map each integer with a corresponding character using a numerical code. The most common numerical code is [[ASCII]], which stands for American Standard Code for Information Interchange.

The following table illustrates the [[ASCII]] code:
![[Pasted image 20230330075822.png]]

For example, the integer number `65` represents a character `A` in upper case.

---
**Nota:**
In C, the `char` type has a 1-byte unit of memory so it is more than enough to hold the ASCII codes. Besides ASCII code, there are various numerical codes available such as extended ASCII codes. Unfortunately, many character sets have more than 127 even 255 values. Therefore, to fulfill those needs, Unicode was created to represent various available character sets. Unicode currently has over 40,000 characters.

---
