---
created: 2023-03-30
type: Programming Note
programming language: "[[C MOC]]"
related:
  - "[[C strlen Function]]"
  - "[[C sizeof Function]]"
  - "[[C While Loops]]"
completed: true
updated: 2024-05-27T13:29
---
---

# How To Calculate The Lenght Of A String In C

# [[C strlen Function]]
In C, you can calculate the length of a string using the `strlen()` function, which is defined in the `string.h` header file.

Here's an example:
```c
#include <stdio.h> 
#include <string.h>

int main() {     c
	har str[100] = "Hello, world!";     
	int length = strlen(str);      
	printf("The length of the string is %d\n", length); 
	// Output: "The length of the string is 13"      
	return 0; 
}
```
In this example, we declare a character array `str` with the value "Hello, world!". We then use the `strlen()` function to calculate the length of the string and store it in an integer variable `length`. Finally, we print the value of `length` using `printf()`. The output is "The length of the string is 13", which is the number of characters in the string excluding the null terminator `\0`.

## How to create the strlen funcTion manually 

### [[C While Loops]] Method:

Here's an example of how to do it:
```c
`#include <stdio.h>  
int main() {     
	char str[100] = "Hello, world!";     
	int length = 0;      // Iterate through the characters in the string until we reach the null terminator     
	while (str[length] != '\0') {         
		length++;     
	}      
	printf("The length of the string is %d\n", length); 
	// Output: "The length of the string is 13"      
return 0; 
}
```
In this example, we declare a character array `str` with the value "Hello, world!". We then initialize an integer variable `length` to 0. We use a while loop to iterate through the characters in the string until we reach the null terminator `\0`. Inside the loop, we increment the value of `length` for each character we encounter.

Once the loop has finished, `length` contains the number of characters in the string, excluding the null terminator. Finally, we print the value of `length` using `printf()`. The output is "The length of the string is 13", which is the number of characters in the string excluding the null terminator.

### [[C sizeof Function]] Method:
If you want to use `sizeof()` to calculate the length of a string, you can divide the size of the array by the size of a character using the `sizeof(char)` operator. However, note that this method assumes that the string is properly null-terminated and that there are no unused elements in the array.

```c
#include <stdio.h>  
int main() {     
	char str[100] = "Hello, world!";     
	int length = sizeof(str) / sizeof(char) - 1; 
	// Subtract 1 to exclude the null terminator      
	printf("The length of the string is %d\n", length); 
	// Output: "The length of the string is 13"      
	return 0; 
}
```

In this example, we declare a character array `str` with the value "Hello, world!". We then use `sizeof()` to calculate the size of the array in bytes and divide it by the size of a character using `sizeof(char)`. We subtract 1 from the result to exclude the null terminator from the length calculation. Finally, we store the length in an integer variable `length` and print its value using `printf()`. The output is "The length of the string is 13", which is the length of the string excluding the null terminator.


### which is the fastest way to mesure a str length ?

**Using Strlen():**
The `strlen()` function is typically implemented using machine code instructions that can quickly scan the memory for the null terminator character that marks the end of the string. This allows the function to compute the length of the string in constant time, regardless of the length of the string.

**Using while:**
In contrast, manually iterating through the string to count the characters can take linear time, which means the execution time increases linearly with the length of the string. This can be slower than using `strlen()` for long strings.

**Using Sizeof:**
Using the `sizeof()` method to calculate the length of a string is generally slower than using the `strlen()` function, because `sizeof()` calculates the size of the array in bytes, which includes any unused elements and the null terminator, whereas `strlen()` only counts the characters up to the null terminator.

If you divide the size of the array by the size of a character using `sizeof(char)` to get the length of the string, you will also need to subtract 1 to exclude the null terminator, which requires an additional operation.

Additionally, using `sizeof()` to calculate the length of a string assumes that the string is properly null-terminated and that there are no unused elements in the array, which may not always be the case. In contrast, `strlen()` explicitly checks for the null terminator and returns an error if it is not found.

#### Use strlen() funcion
Overall, while `sizeof()` can be used to calculate the length of a string, it is generally not as efficient as using `strlen()`. For best performance, you should use `strlen()` to measure the length of a null-terminated string in C.