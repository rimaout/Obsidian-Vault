---
created: 2023-03-28
type: Programming Note
programming language: "[[C MOC]]"
related: 
completed: true
updated: 2024-05-27T13:29
---
---
In programming, a loop is used to repeat a block of code until the specified condition is met.

---
# For Loop
When you know exactly how many times you want to loop through a block of code, use the `for` loop instead of a [[C While Loops]]

## Syntax
```c
for (initializationStatement; testExpression; updateStatement)
{
    // statements inside the body of loop
}
```

### How for loop works?

- The initialization statement is executed only once.
- Then, the test expression is evaluated. If the test expression is evaluated to false, the `for` loop is terminated.
- However, if the test expression is evaluated to true, statements inside the body of the `for` loop are executed, and the update expression is updated.
- Again the test expression is evaluated.

This process goes on until the test expression is false

**Note:** `testExpression` it's made by [[C Comparison Operators]] and [[C Logical Operators]].

### For loop Flowchart
![[Pasted image 20230328092226.png]]

### Example 1:
```c
// Print numbers from 1 to 10
#include <stdio.h>

int main() {
  int i;

  for (i = 1; i < 11; ++i)
  {
    printf("%d ", i);
  }
  return 0;
}
```
**Output:** `1 2 3 4 5 6 7 8 9 10`

### Example 2: 
```c
// Program to calculate the sum of first n natural numbers
// Positive integers 1,2,3...n are known as natural numbers

#include <stdio.h>
int main()
{
    int num, count, sum = 0;

    printf("Enter a positive integer: ");
    scanf("%d", &num);

    // for loop terminates when num is less than count
    for(count = 1; count <= num; ++count)
{
        sum += count;
    }

    printf("Sum = %d", sum);

    return 0;
}
```
**Oputput:** `Sum = 55`

---
