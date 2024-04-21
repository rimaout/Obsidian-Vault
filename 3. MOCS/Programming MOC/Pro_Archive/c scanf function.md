---
Created: 2023-03-22
Type: Programming Note
Programming Language: "[[C MOC]]"
Related:
  - "[[C User Input]]"
Completed: true
---
---
## Index
1. [[#Single Input]]
2. [[#Multiple Input]]
3. [[#Take String Input]]
4. [[#`scanf` Limitations]]
	-  [[#**kikketta** To Solve `scanf` Limitations|Trick to solove scanf limitation]]

---
## Single Input

To get **user input**, you can use the `scanf()` function, example:
```C
// Create an integer variable that will store the number we get from the user  
int myNum;  
  
// Ask the user to type a number  
printf("Type a number: \n");  
  
// Get and save the number the user types  
scanf("%d", &myNum);  
  
// Output the number the user typed  
printf("Your number is: %d", myNum);
```

- The `scanf()` function takes two arguments: 
	1. the **[[C Format Specifiers]]** of the variable
	2. the **[[C Variables And Constants]]** where the input will be saved

**oss:** if the input is not accepted, the variable won’t be saved
**oss:** you can specify the input text
```c
scanf("(%d-%d)", %x, %y);
```
The input from the user must follow the same sintax:
```txt
(12-13)
```

>[! warning] Note:
it's better to not inset spaces inside the scanf sintax

---
## Multiple Input

The `scanf()` function also allow multiple inputs (an integer and a character in the following example):
``` C
// Create an int and a char variable  
int myNum;  
char myChar;  
  
// Ask the user to type a number AND a character  
printf("Type a number AND a character and press enter: \n");  
  
// Get and save the number AND character the user types  
scanf("%d %c", &myNum, &myChar);
  
// Print the number  
printf("Your number is: %d\n", myNum);  
  
// Print the character  
printf("Your character is: %c\n", myChar);
```

---
## Take String Input

You can also get a string entered by the user:
```C
// Create a string  
char firstName[30];  
  
// Ask the user to input some text  
printf("Enter your first name: \n");  
  
// Get and save the text  
scanf("%s", firstName);  
  
// Output the text  
printf("Hello %s", firstName);
```

>[! warning] Note:
>When working with strings in `scanf()`:
>- you must specify the size of the string/array  
>- you don't have to use the reference operator (`&`).

---
## `scanf` Limitations 

scanf considers space (whitespace, tabs, etc) as a **terminating character**, 
- which means that it can only display a single word (even if you type many words). 

Example:
```C
char fullName[30];  
  
printf("Type your full name: \n");  
scanf("%s", &fullName);  
  
printf("Hello %s", fullName);  
  
// Type your full name: John Doe  
// Hello John
```
From the example above, you would expect the program to print "John Doe", but it only prints "John".

---
### **kikketta** To Solve `scanf` Limitations
Using this metod you can reed more of one word at the time
```c
#include <stdio.h>

int main() 
{
	char line[100];
	
	printf("Enter a line of text: ");
	scanf("%[^\n]", line);
	printf("You entered: %s\n", line);
	
	return 0;
}
```
In this example, we declare a character array `line` of size 100 to store the user's input. We use the `%[^\n]` format specifier to read a string with spaces, which tells `scanf` to read all characters up to (but not including) a newline character (`'\n'`).

>[!warning] Note:
>We are basicly ignoring all escaping character but not inlcluding `\n` (new line)

---