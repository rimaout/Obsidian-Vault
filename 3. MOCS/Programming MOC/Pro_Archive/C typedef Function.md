---
created: 2023-03-30
type: Programming Note
programming language: "[[C MOC]]"
related:
  - "[[C Embedded  Functions]]"
  - "[[C Variables And Constants]]"
completed: true
updated: 2024-05-27T13:29
---
---
# typedef()
The `typedef` keyword is used to create a new type definition:

## Syntax:
```c
typedef existing_type new_type_name;
```

## Example:
```c
#include <stdio.h>  
typedef int my_int;  

int main() {   
	my_int x = 5;   
	printf("%d\n", x);   
	
	return 0; }`
```
In this example, we use `typedef` to create a new type `my_int` which is an alias for `int`. We then declare a variable `x` of type `my_int` and initialize it to the value 5. Finally, we print the value of `x` using `printf()`.

---
## Benefits:
Using `typedef` can make code more readable and maintainable by giving meaningful names to data types. It also allows for easier modification of types throughout the codebase.

---
## Usage:

**To create a new type alias for an existing type:**
```c
typedef existing_type new_type_name;
```

**To create a new type alias for a pointer type:**
```c
typedef existing_type* new_type_name;
```

**To create a new type alias for a function pointer:**
```c
typedef return_type (*new_type_name)(argument_types);
```

**To create a new type alias for a struct:**
```c
typedef struct struct_name new_type_name;
```

**To create a new type alias for an enum:**
```c
typedef enum enum_name new_type_name;
```

