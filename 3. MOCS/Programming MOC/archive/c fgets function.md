---
created: 2023-03-12
type: Programming Note
programming language: "[[C MOC]]"
related: 
completed: true
updated: 2024-05-27T13:29
---
---
## Index
1. [[#`fgets` Function]]
2. [[#`fgets` Limitation Null termination]]

---
## `fgets` Function
You can use `fgets()` function is used to read a line of text from a file or input from the user. 

It is declared in the `stdio.h` header file as follows:
```c
char *fgets(char *str, int n, FILE *stream);
```

The function takes **three arguments**:
-   `str`: a pointer to the buffer where the line of text is stored
-   `n`: the maximum number of characters to read
-   `stream`: a pointer to the input stream to read from

The `fgets` function **reads characters from the input stream until:**
- it encounters a newline character (`'\n'`)
- it encounters the end-of-file indicator (`EOF`)
- it has reached the maximum numbers of characters that can be stored in the variable (`sizeof(fullName) - 1`).
	- in the example above: (30 -1) 
 
**User Input Example:**
```C
char fullName[30];  
  
printf("Type your full name: \n");  
fgets(fullName, sizeof(fullName), stdin);  
  
printf("Hello %s", fullName);  
  
// Type your full name: John Doe  
// Hello John Doe
```

**File Input Example:**
```c
#include <stdio.h>

int main() 
{
    char buffer[100];
    FILE *fp = fopen("example.txt", "r");
    if (fp == NULL) {
        printf("Failed to open file\n");
        return 1;
    }
    while (fgets(buffer, 100, fp) != NULL) {
        printf("%s", buffer);
    }
    fclose(fp);
    return 0;
}
```
This program opens a file named "example.txt" for reading, then reads lines from the file using `fgets` and prints them to the console using `printf`. Note that `fgets` reads at most `100-1` characters at a time to avoid buffer overflow.

---
### `fgets` Limitation: Null termination

`fgets` appends a null character (`'\0'`) to the end of the string it reads, so:
- the buffer passed to `fgets` must be large enough to accommodate the null character.
---