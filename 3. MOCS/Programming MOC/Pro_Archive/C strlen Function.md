---
created: 2023-03-30
type: Programming Note
programming language: "[[C MOC]]"
related:
  - "[[C Embedded  Functions]]"
  - "[[How To Get Stringh Lenght In C]]"
completed: true
updated: 2024-05-27T13:29
---
---

**Function signature:** `size_t strlen(const char *str);`

**Function description:** The `strlen()` function computes the length of the null-terminated string `str`.

**Function return value:** The length of the string, not including the null terminator.

**Funcion computational cost:** generally O(n)

**Library:** string.h 

**Function example:**
```c 
#include <stdio.h> 
#include <string.h>  
int main() {     
	char str1[] = "Hello, world!";     
	char str2[] = "";     
	char *str3 = "This is a test string.";     
	
	size_t len1 = strlen(str1);     
	size_t len2 = strlen(str2);     
	size_t len3 = strlen(str3);      
	
	printf("Length of str1: %zu\n", len1); 
	printf("Length of str2: %zu\n", len2); 
```
The output is:
```
Length of str1: 13 
Length of str2: 0 
Length of str3: 22
```

In this example, we declare three strings: `str1`, `str2`, and `str3`. We then use `strlen()` to compute the length of each string and store the results in integer variables `len1`, `len2`, and `len3`. Finally, we print the length of each string using `printf()`.

# Funcion Computational Cost
The computational cost of `strlen()` is O(n), where n is the length of the input string, and increases linearly with the length of the string. However, the function is highly optimized for performance, so its execution time is usually negligible.