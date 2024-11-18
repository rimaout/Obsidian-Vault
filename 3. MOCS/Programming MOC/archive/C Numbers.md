---
created: 2024-03-26
type: Programming Note
programming language: "[[C MOC]]"
related: 
completed: true
updated: 2024-05-27T13:29
---
---
# int
We can use `int` for declaring an integer variable:
```c
int num;
```

|Type|Storage size| Value range| 
|---|---|---|
|**Char**|1 byte |-128 to 127 or 0 to 255| 
|**unsigned char**| 1 byte |0 to 255|
|**signed char** |1 byte| -128 to 127 |
|**Int**| 2 or 4 bytes |-32,768 to 32,767 or -2,147,483,648 to 2,147,483,647| |unsigned int| 2 or 4 bytes|0 to 65,535 or 0 to 4,294,967,295 |
|**Short** |2 bytes| -32,768 to 32,767 |
|**unsigned short**| 2 bytes |0 to 65,535 |
|**Long**| 4 bytes| -2,147,483,648 to 2,147,483,647 |
|**unsigned long**| 4 bytes| 0 to 4,294,967,295 |

>To get the exact size of a type or a variable on a particular platform, you 
> can use the **sizeof** operator.

# float

```c
float num;
```

In C, floating-point numbers can also be represented in exponential. For example:
```c
float normalizationFactor = 22.442e2;
```

|Type |Storage size |Value range |Precision|
|---|---|---|---|
|**float**| 4 byte |1.2E-38 to 3.4E+38 |6 decimal places |
|**double** |8 byte |2.3E-308 to 1.7E+308 |15 decimal places |
|**long double**| 10 byte |3.4E-4932 to 1.1E+4932 |19 decimal places|

## Set Decimal Precision
You have probably already noticed that if you print a floating point number, the output will show many digits after the decimal point:

**Example:**
``` c
float myFloatNum = 3.5;  
double myDoubleNum = 19.99;  
  
printf("%f\n", myFloatNum); // Outputs 3.500000  
printf("%lf", myDoubleNum); // Outputs 19.990000
```

If you want to remove the extra zeros (set decimal precision), you can use a dot (`.`) followed by a number that specifies how many digits that should be shown after the decimal point:

**Example:**
```c
float myFloatNum = 3.5;  
  
printf("%f\n", myFloatNum); // Default will show 6 digits after the decimal point  
printf("%.1f\n", myFloatNum); // Only show 1 digit  
printf("%.2f\n", myFloatNum); // Only show 2 digits  
printf("%.4f", myFloatNum);   // Only show 4 digits
```
# Aritmetic operations on numbers
[[C Arithmetic Operators]]
[[C Increment and Decrement Operators]]

# Type Conversation
[[C Num Type Conversion]]

# Number Comparioson
[[C Comparison Operators]]

# Number 
[[C Assignment Operators]]