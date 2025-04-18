---
type: Programming Note
programming language: "[[C MOC]]"
related: 
completed: false
created: 2025-04-18T17:20
updated: 2025-04-18T17:26
---
Lo specificatore di formato (format specifier)  è un carattere speciale utilizzato per indicare il tipo di dato che verrà stampato (print) e letto (scanf)

| Type                   | Format Specifier |
| ---------------------- | ---------------- |
| **int**                | `%d`, `%i`       |
| **char**               | `%c`             |
| **float**              | `%f`             |
| **double**             | `%lf`            |
| short int              | `%hd`            |
| unsigned int           | `%u`             |
| long int               | `%ld`, `%li`     |
| long long int          | `%lld`, `%lli`   |
| unsigned long int      | `%lu`            |
| unsigned long long int | `%llu`           |
| signed char            | `%c`             |
| unsigned char          | `%c`             |
| long double            | `%Lf`            |

>[!note] Esempio print
>
>```c
>int a = 10; 
>float b = 3.14;
>
>printf("The value of a is %d and the value of b is %f", a, b);`
>```
>
>Utilizziamo `%d` e `%d` per indicare rispettivamente che dobbiamo stampare un `integr` e un `floating-point`.

>[!note] Esempio scanf
>
>``` c
>   int age;
>   char name[20];
>   
>   printf("Enter your age: ");
>   scanf("%d", &age); // using %d format specifier to read integer input
>```
