---
Created: 2023-03-26
Type: Programming Note
Programming Language: "[[C MOC]]"
Related: 
Completed: true
---
---
The data type specifies the size and type of information the variable will store

| Type | Size (bytes) | Format Specifier |
| --- | --- | --- |
| **int** | at least 2, usually 4 | %d, %i |
| **char** | 1 | %c |
| **float** | 4 | %f |
| **double** | 8 | %lf |
| short int | 2 usually | %hd |
| unsigned int | at least 2, usually 4 | %u |
| long int | at least 4, usually 8 | %ld, %li |
| long long int | at least 8 | %lld, %lli |
| unsigned long int | at least 4 | %lu |
| unsigned long long int | at least 8 | %llu |
| signed char | 1 | %c |
| unsigned char | 1 | %c |
| long double | at least 10, usually 12 or 16 | %Lf |

- More information about [[C Format Specifiers]]

### int [[C Numbers]]

Integers are whole numbers that can have both zero, positive and negative values but no decimal values. For example, `0`, `-5`, `10`

We can use `int` for declaring an integer variable.

```c
int id;
```

Here, id is a variable of type integer.

You can declare multiple variables at once in C programming.

```c
int id, age;
```
The size of `int` is usually 4 bytes (32 bits). And, it can take `232` distinct states from `-2147483648` to `2147483647`.

---

### float and double [[C Numbers]]

`float` and `double` are used to hold real numbers.
```c
float salary;
double price;
```

In C, floating-point numbers can also be represented in exponential. 
```c
float normalizationFactor = 22.442e2;
```

What's the difference between `float` and `double`?

The size of `float` (single precision float data type) is 4 bytes. And the size of `double` (double precision float data type) is 8 bytes.

---

### char [[C Chars]]

Keyword `char` is used for declaring character type variables.
```c
char test = 'h';
```

---

### void
- `void` is an **incomplete type**. 
- It means "nothing" or "no type". You can think of void as **absent**.

For example, if a function is not returning anything, its return type should be `void`

>[!warning]
>Note that, you cannot create variables of `void` type.

---

### long
If you need to use a large number, you can use a type specifier `long`. Here's how:
``` c
long a;
long long b;
long double c;
```
Here variables a and b can store integer values. And, c can store a floating-point number.

### short
If you are sure, only a small integer (`[−32,767, +32,767]` range) will be used, you can use `short`:
```c
short d;
```

---

### signed and unsigned

In C, `signed` and `unsigned` are type modifiers. You can alter the data storage of a data type by using them:
-   `signed` - allows for storage of both positive and negative numbers
-   `unsigned` - allows for storage of only positive numbers

``` c
// valid codes
unsigned int x = 35;
int y = -35;  // signed int
int z = 36;  // signed int

// invalid code: unsigned int cannot hold negative integers
unsigned int num = -35;
```
Here, the variables x and num can hold only zero and positive values because we have used the `unsigned` modifier.

Considering the size of `int` is 4 bytes, variable y can hold values from `-231` to `231-1`, whereas variable x can hold values from `0` to `232-1`