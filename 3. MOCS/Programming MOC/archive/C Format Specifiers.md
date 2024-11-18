---
created: 2023-02-26
type: Programming Note
programming language: "[[C MOC]]"
related: 
completed: true
updated: 2024-05-27T13:29
---
---
In C programming, a format specifier is a **special character that is used to specify the type of data that will be printed or read** in a formatted input/output operation. 

Format specifiers are used in conjunction with the [printf()](C%20Print%20Output.md) and [scanf()](C%20User%20Input.md) functions to format the input and output of data.

**Here are some commonly used format specifiers in C:**

| Type | Format Specifier |
| --- |  --- |
| int |%d, %i |
| char | %c |
| float |  %f |
| double |  %lf |
| short int  | %hd |
| unsigned int | %u |
| long int | %ld, %li |
| long long int  | %lld, %lli |
| unsigned long int | %lu |
| unsigned long long int |  %llu |
| signed char |  %c |
| unsigned char |  %c |
| long double |  %Lf |

**printf() example:** 
```c
int a = 10; 
float b = 3.14;

printf("The value of a is %d and the value of b is %f", a, b);`
```
In this code, the format specifiers %d and %f are used to print the integer and floating-point values of a and b, respectively.

**scanf() example:**
``` c
   int age;
   char name[20];
   
   printf("Enter your age: ");
   scanf("%d", &age); // using %d format specifier to read integer input
```