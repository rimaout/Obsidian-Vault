---
created: 2023-03-27
type: Programming Note
programming language: "[[Python MOC]]"
related: 
completed: true
updated: 2024-05-27T13:29
---
---
A relational operator checks the relationship between two operands. If the relation is true, it returns 1; if the relation is false, it returns value 0.

Relational operators are used in [decision making](C%20If%20...%20Else.md) and loops ([[C For Loops]], [[C While Loops]])

|Operator|Meaning of Operator|Example|
|---|---|---|
|== |Equal to |`5 == 3` is evaluated to 0|
|>|Greater than|`5 > 3` is evaluated to 1|
|<|Less than|`5 < 3` is evaluated to 0|
|!=|Not equal to|`5 != 3` is evaluated to 1|
|>=|Greater than or equal to|`5 >= 3` is evaluated to 1|
|<=|Less than or equal to|`5 <= 3` is evaluated to 0|

##  C Relational Operators Using [[C Arrays]]
- Relational operators can also be used to compare arrays in C. 
- When comparing arrays, the comparison is done element by element, starting from the first element of each array, until a difference is found. 
- The result of the comparison is determined by the comparison of the corresponding elements.

>[!warning]
>The elements of the arrays must be of the **same data type**.

## C Relational Operators Using [[C Chars]]
- When comparing characters, the [[comparison]] is based on their [[ASCII]] values.

- The ASCII table assigns a unique numerical value to each character, and

## C Relational Operators Using [[C Strings]]
- When using relational operators with strings, the comparison is based on the [[ASCII]] values of the characters in the strings.

- The comparison is done character by character, starting from the leftmost character, until a difference is found. 
- The result of the comparison is determined by the ASCII value of the characters being compared.