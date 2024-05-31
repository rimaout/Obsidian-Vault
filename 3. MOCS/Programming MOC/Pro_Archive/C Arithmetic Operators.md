---
created: 2022-03-27
type: Programming Note
programming language: "[[C MOC]]"
related: 
completed: true
updated: 2024-05-27T13:29
---
---
# Operators
An arithmetic operator performs mathematical operations such as addition, subtraction, multiplication, division etc on numerical values (constants and variables).

|Operator| Meaning of Operator |
|---|---|
| + | addition or unary plus|
| - | subtraction or unary minus|
| * | multiplication |
| / |division |
|% | remainder after division (modulo division) |

# Arithmetic Operations On Numbers
``` c
    int a = 9,b = 4, c;
    
    c = a + b; // Output: 13
    c = a - b; // Output: 5
    c = a * b; // Output: 36
    c = a / b; // Output: 2
    c = a % b; // Output: 1
```

>[!warning]
> - The `%` operator can only be used with integers. 
> - When using the `/` operator the result will be an integer if bought the values are integers

### Strange Case
In normal calculation, `9/4 = 2.25`. However, the output is `2` in the program.

It is because **both the variables a and b are integers**. Hence, the output is also an integer. The compiler neglects the term after the decimal point and shows answer `2` instead of `2.25`.

**Read more:** [[C Num Type Conversion#Strange Case:]]

**Example:**
```c
a = 5.0;
b = 2.0;
c = 5;
d = 2; 
// Either one of the operands is a floating-point number
a/b = 2.5  
a/d = 2.5  
c/b = 2.5  

// Both operands are integers
c/d = 2
```


## Arithmetic Operators On Arrays Of Numbers
*You cannot use arithmetic operators on arrays of numbers directly in C.*

In C, an array is a collection of elements of the same data type. To perform arithmetic operations on the elements of an array, you need to access each element individually and perform the operation.

Here's an example of how you can add two arrays of integers in C:
```c
#include <stdio.h>  ù
int main() {     
	int arr1[] = {1, 2, 3, 4, 5};     
	int arr2[] = {6, 7, 8, 9, 10};     
	int result[5];      

	for (int i = 0; i < 5; i++) {         
		result[i] = arr1[i] + arr2[i];     
}     
	printf("Result: ");    
	 
	for (int i = 0; i < 5; i++) {         
		printf("%d ", result[i]);     
}        

	return 0; 
}
```
So while you cannot perform arithmetic operations on arrays directly in C, you can iterate over the elements of an array and perform operations on each element individually.

## Arithmetic Operators On [[C Chars]]
The arithmetic operators, when used with `char` variables, they perform arithmetic operations on their [[ASCII]] values, which are represented as integers.

For example:
```c
char a = 'a';
char b = 'b';
char c = a + b; // This will perform the arithmetic operation on the ASCII values of 'a' and 'b'
```

## Arithmetic Operators On [[C Strings]]
- Arithmetic operators are not designed to work with strings, which are [[C Arrays]] of characters.