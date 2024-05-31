---
created: 2023-03-22
type: Programming Note
programming language: "[[C MOC]]"
related: 
completed: true
updated: 2024-05-27T13:29
---
---
Variables are containers for storing data values, like numbers and characters.

## Declaring (Creating) Variables
To create a variable, specify the **[[C Data Types]]** and assign it a **value**:

### Syntax
```c
type variableName = value;
```

You can also declare a variable without assigning the value, and assign the value later:
```c
// Declare a variable  
int myNum;  
  
// Assign a value to the variable  
myNum = 15;
```

## Variable Names

All C **variables** must be identified with **unique names**, these unique names are called **identifiers**.

**Naming Rules:**
1.  A variable name can only have letters (both uppercase and lowercase letters), digits and underscore.
2.  The first letter of a variable should be either a letter or an underscore.

## Output Variables
You learned from [[C Print Output]] that you can output values/print text with the `printf()` function:

In many other programming languages, you would normally use a print function to display the value of a variable. However, this is **not possible in C**:
```c
int myNum = 15;  
printf(myNum);  // Nothing happens
```

To output variables in C, you must get familiar with something called "[[C Format Specifiers]]

### Syntax
```c
printf("format specifier", variable );
```

## Change Variable Values

**Note:** If you assign a new value to an existing variable, it will overwrite the previous value:

```c
int myNum = 15;  // myNum is 15  
myNum = 10;  // Now myNum is 10
```

## Assign Values
You can also assign the value of one variable to another:

```c
int myNum = 15;  
  
int myOtherNum = 23;  
  
// Assign the value of myOtherNum (23) to myNum  
myNum = myOtherNum;  
  
// myNum is now 23, instead of 15
```

---
## Constants

If you want to define a variable whose value cannot be changed, you can use the `const` keyword. This will create a constant. For example,

``` c
const double PI = 3.14;
```
---