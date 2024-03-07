Tag: [[Programming MOC]], [[C MOC]]

---

# Increment ++ and Decrement -- Operator as Prefix and Postfix

In programming (Java, C, C++, JavaScript etc.), the increment operator `++` increases the value of a variable by 1. Similarly, the decrement operator `--` decreases the value of a variable by 1.
```c
a = 5

++a;          // a becomes 6
a++;          // a becomes 7
--a;          // a becomes 6
a--;          // a becomes 5
```
Simple enough till now. However, there is an important difference when these two operators are used as a prefix and a postfix.

---

## ++ and -- operator as prefix and postfix

-   If you use the `++` operator as a **prefix** like: `++var`, the value of var is incremented by 1; then it returns the value.
-   If you use the `++` operator as a **postfix** like: `var++`, the original value of var is returned first; then var is incremented by 1.

The `--` operator works in a similar way to the `++` operator except `--` decreases the value by 1.

Let's see the use of `++` as prefixes and postfixes in C, C++, Java and JavaScript.

---

## Example: [[C MOC]] Programming

```c
#include <stdio.h>
int main() {
   int var1 = 5, var2 = 5;

   // 5 is displayed
   // Then, var1 is increased to 6.
   printf("%d\n", var1++);

   // var2 is increased to 6 
   // Then, it is displayed.
   printf("%d\n", ++var2);

   return 0;
}
```

---

## Example: [[C++]]

``` c++
#include <iostream>

using namespace std;

int main() {
   int var1 = 5, var2 = 5;

   // 5 is displayed
   // Then, var1 is increased to 6.
   cout << var1++ << endl;

   // var2 is increased to 6
   // Then, it is displayed.
   cout << ++var2 << endl;

   return 0;
}
```

---

## Example: [[Java]] Programming

```Java
class Operator {
    public static void main(String[] args) {
        int var1 = 5, var2 = 5;

        // 5 is displayed
        // Then, var1 is increased to 6.
        System.out.println(var1++);

        // var2 is increased to 6
        // Then, var2 is displayed
        System.out.println(++var2);
    }
}
```

---

## Example 4: [[JavaScript]]

```JavaScript
let var1 = 5, var2 = 5;

// 5 is displayed
// Then, var1 is increased to 6
console.log(var1++)

// var2 is increased to 6
// Then, var2 is displayed
console.log(++var2)
```

The output of all these programs will be the same.
**Output**
5
6


---