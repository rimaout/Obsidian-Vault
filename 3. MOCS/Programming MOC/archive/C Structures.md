---
created: 2023-04-11
type: Programming Note
programming language: "[[C MOC]]"
related: 
completed: true
updated: 2025-03-26T13:47
---
---
## Define Structures
In C programming, a struct (or structure) is a collection of [variables](C%20Variables%20And%20Constants.md) (can be of different types) under a single name.

### Syntax
```c
struct structureName {
  dataType member1;
  dataType member2;
  ...
};
```

**Example:**
```c
struct Person {
  char name[50];
  int citNo;
  float salary;
};
```

---

## Create struct Variable
When a `struct` type is declared, no storage or memory is allocated. To allocate memory of a given structure type and work with it, we need to create variables.

**Here's how we create structure variables:**
```c
struct Person {
  char[] name;
  int salary;
};

int main() {
  struct Person name = "Matteo", salary = 5000;
  return 0;
}
```

Another way of creating a `struct` variable is:
```c
struct Person {
  char[] name;
  int salary;
} name = "Matteo", salary = 5000;
```

In both cases:
-   `person1` and `person2` are `struct Person` variables
-   `p[]` is a `struct Person` array of size 20.

---

## Access Members of a Structure

There are two types of operators used for accessing members of a structure.

1.  `.` - Member operator
2.  `->` - Structure pointer operator (reed [[C Pointers and Structures]])

Suppose, you want to access the salary of person2. Here's how you can do it:
```c
person2.salary
```

### Example C structs:

```c
#include <stdio.h>
#include <string.h>

// create struct with person1 variable
struct Person {
  char name[50];
  int citNo;
  float salary;
} person1;

int main() {

  // assign value to name of person1
  strcpy(person1.name, "George Orwell");

  // assign values to other person1 variables
  person1.citNo = 1984;
  person1. salary = 2500;

  // print struct variables
  printf("Name: %s\n", person1.name);
  printf("Citizenship No.: %d\n", person1.citNo);
  printf("Salary: %.2f", person1.salary);

  return 0;
}
```

**Output:**
``` txt
Name: George Orwell
Citizenship No.: 1984
Salary: 2500.00
```

---

## Keyword typedef

We use the [[C typedef Function]] keyword to create an alias name for data types. It is commonly used with structures to simplify the syntax of declaring variables.

**Example:**

```c
struct Distance{
  int feet;
  float inch;
};

int main() {
  struct Distance d1, d2;
}
```

We can use `typedef` to write an equivalent code with a simplified syntax:
```c
typedef struct Distance {
  int feet;
  float inch;
} distances;

int main() {
  distances d1, d2;
}
```

---

### Example: C typedef

```c
#include <stdio.h>
#include <string.h>

// struct with typedef person
typedef struct Person {
  char name[50];
  int citNo;
  float salary;
} person;

int main() {

  // create  Person variable
  person p1;

  // assign value to name of p1
  strcpy(p1.name, "George Orwell");

  // assign values to other p1 variables
  p1.citNo = 1984;
  p1. salary = 2500;

  // print struct variables
  printf("Name: %s\n", p1.name);
  printf("Citizenship No.: %d\n", p1.citNo);
  printf("Salary: %.2f", p1.salary);

  return 0;
}
```

**Output:**
``` txt
Name: George Orwell
Citizenship No.: 1984
Salary: 2500.00
```

---

## Nested Structures

You can create structures within a structure in C programming.

**Example:**
``` c
struct complex {
  int imag;
  float real;
};

struct number {
  struct complex comp;
  int integers;
} num1, num2;
```

Suppose, you want to set `imag` of `num2` variable to **11**. Here's how you can do it:
```c
num2.comp.imag = 11;
```

---

### Example 3: C Nested Structures

```c
#include <stdio.h>

struct complex {
  int imag;
  float real;
};

struct number {
  struct complex comp;
  int integer;
} num1;

int main() {

  // initialize complex variables
  num1.comp.imag = 11;
  num1.comp.real = 5.25;

  // initialize number variable
  num1.integer = 6;
	
  // print struct variables
  printf("Imaginary Part: %d\n", num1.comp.imag);
  printf("Real Part: %.2f\n", num1.comp.real);
  printf("Integer: %d", num1.integer);

  return 0;
}
```

**Output**
```tx
Imaginary Part: 11
Real Part: 5.25
Integer: 6
```

---
