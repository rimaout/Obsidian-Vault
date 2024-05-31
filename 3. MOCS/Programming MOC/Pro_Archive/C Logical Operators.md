---
created: 2023-03-28
type: Programming Note
programming language: "[[C MOC]]"
related: 
completed: true
updated: 2024-05-27T13:29
---
---

- An expression containing logical operator returns either 0 or 1 depending upon whether expression results true or false. 
- Logical operators are commonly used in [[C If ... Else]], [[C For Loops]], [[C While Loops]]

|Operator|Name|Meaning|Example|
|---|---|---|---|
|&&|Logical AND| Returns true if both statements are true|x < 5 &&  x < 10|
|\|\||Logical OR| Returns true if one of the statements is true|x < 5 \|\| x < 4
|!|Logical NOT|Reverse the result, returns false if the result is true|!(x < 5 && x < 10)|

```c
    int a = 5, b = 5, c = 10, result;


    result = (a == b) && (c > b); // Output: 1

    result = (a == b) && (c < b); // Output: 0

    result = (a == b) || (c < b); // Output: 1

    result = (a != b) || (c < b); // Output: 0

    result = !(a != b); // Output: 1

    result = !(a == b); // Output: 0
```