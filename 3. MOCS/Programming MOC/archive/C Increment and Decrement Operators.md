---
created: 2023-03-27
type: Programming Note
programming language: "[[C MOC]]"
related: 
completed: true
updated: 2024-05-27T13:29
---



---
## C Increment and Decrement Operators 

C programming has two operators increment `++` and decrement `--` to change the value of an operand (constant or variable) by 1.

Increment `++` increases the value by 1 whereas decrement `--` decreases the value by 1. These two operators are unary operators, meaning they only operate on a single operand.

**Example:**
```c

    int a = 10, b = 100;
    float c = 10.5, d = 100.5;

    printf("++a = %d \n", ++a); // Output: 11
    printf("--b = %d \n", --b); // Output: 99
    printf("++c = %f \n", ++c); // Output: 11.5
    printf("--d = %f \n", --d); // Output: 99.5

```

Here, the operators `++` and `--` are used as prefixes. These two operators can also be used as postfixes like `a++` and `a--`. Visit this page to learn more about how [increment and decrement operators work when used as postfix](https://www.programiz.com/article/increment-decrement-operator-difference-prefix-postfix "Increment Operator as postfix").

## C Increment and Decrement Operators  on Chars
In C, characters can be treated as integers and can be incremented and decremented just like integers. The increment operator `++` and decrement operator `--` can be used with characters to increase or decrease their ASCII code values.

**Example:**
```c
char ch = 'A'; ch++;  // increment ch by 1 
printf("%c", ch);  // outputs 'B'
```

```c
char ch = 'B'; ch--;  // decrement ch by 1 
printf("%c", ch);  // outputs 'A'
```


>Note that when a character variable is incremented or decremented, its ASCII code value changes, not its character representation. Therefore, incrementing 'z' (which has an ASCII code value of 122) will result in '{' (which has an ASCII code value of 123), not 'a'. Similarly, decrementing 'A' (which has an ASCII code value of 65) will result in '@' (which has an ASCII code value of 64), not 'Z'.