---
Created: 2023-04-27
Type: Programming Note
Programming Language: "[[C MOC]]"
Related:
  - "[[C Embedded  Functions]]"
  - "[[C User Input]]"
Completed: true
---
---
# sscanf() 
This function works the same as the [C scanf Function](C%20User%20Input.md) but instead of inserting the input string from the terminal it has to be passed as the first parameter

**Syntax:**
```c
sscanf(str, format specifiers , variable);
```

The `scanf()` function takes two arguments: 
	1. [[C Strings]]: a sting as a variable or a constant ("example of a constant")
	2. the **[[C Format Specifiers]]** of the variable
	3. the **[[C Variables And Constants|C Variables]]** where the input will be saved

## Single Input

```C
char str[10] = "mamme";
char copy[10];
    
sscanf(str, "%s", copy);

printf("Str: %s\n", str);    // Str: mamme
printf("Copy: %s\n", copy);  // copy: mamme
```
**Nota:** if the input is not accepted, the variable won’t be saved

---
## Multiple Input

The `sscanf()` function also allow multiple inputs (an integer and a character in the following example):
``` C
int day, year;
   char weekday[20], month[20], dtm[100];

   strcpy( dtm, "Saturday March 25 1989" );
   sscanf( dtm, "%s %s %d  %d", weekday, month, &day, &year );

   printf("%s %d, %d = %s\n", month, day, year, weekday );
   // Output: March 25, 1989 = Saturday
```

**oss:** you can specify the input text
```c
char str[] = "(12-13)";
int copy, copy2;

    
sscanf(str, "(%d-%d)", &copy, &copy2);

printf("Str: %s\n", str);      // Str: (12-13)
printf("Copy: %d\n", copy);    // Copy: 12
printf("Copy2: %d\n", copy2);  // Copy: 13
```

**Nota:** if the input is not accepted, the variable won’t be saved
>[! warning] Note:
it's better to not insert spaces inside the scanf syntax


---
