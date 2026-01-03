---
created: 2023-03-26
type: Programming Note
programming language: "[[C MOC]]"
related: 
completed: true
updated: 2024-05-27T13:29
---
---
# Type Conversion

Sometimes, you have to convert the value of one data type to another type. This is known as **[[C Type Conversion]]**.


For example, if you try to divide two integers, `5` by `2`, you would expect the result to be `2.5`. But since we are working with integers (and not floating-point values), the following example will just output `2`:

**Example:**
```c
int x = 5;  
int y = 2;  
int sum = 5 / 2;  
  
printf("%d", sum); // 
```

---

## There are two types of conversion in C:

-   **Implicit Conversion** (automatically)  
    
-   **Explicit Conversion** (manually)

---

## Implicit Conversion

Implicit conversion is done automatically by the compiler when you assign a value of one type to another.

For example, if you assign an `int` value to a `float` type:

**Example:**
```c
// Automatic conversion: int to float  
float myFloat = 9;  
  
printf("%f", myFloat); // 9.000000
```

As you can see, the compiler automatically converts the int value `9` to a float value of `9.000000`.

>[!warning]
>Especially if it was the other way around - the following example automatically converts the float value `9.99` to an int value of `9`:x
```c
// Automatic conversion: float to int  
int myInt = 9.99;  
printf("%d", myInt); // 9
```  
---
## Strange Case:
As another example, if you divide two integers: `5` by `2`, you know that the sum is `2.5`. And as you know from the beginning of this page, if you store the sum as an integer, the result will only display the number `2`. Therefore, it would be better to store the sum as a `float` or a `double`, right?

**Example:**
```c
float sum = 5 / 2;  
  
printf("%f", sum); // 2.000000

```

Why is the result `2.00000` and not `2.5`? Well, it is because 5 and 2 are still integers in the division. In this case, you need to manually convert the integer values to floating-point values. (see below).

---

## Explicit Conversion (casting)

Explicit conversion is done manually by placing the type in parentheses `()` in front of the value.

Considering our problem from the example above, we can now get the right result:
```c
// Manual conversion: int to float  
float sum = (float) 5 / 2;  
  
printf("%f", sum); // 2.500000
```

You can also place the type in front of a variable:
```c
int num1 = 5;  
int num2 = 2;  
float sum = (float) num1 / num2;  
  
printf("%f", sum); // 2.500000
```