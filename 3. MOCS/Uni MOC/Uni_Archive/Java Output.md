---
Created: 2024-03-08
Type: "[[🏫 Programming MOC]]"
Programming Language: "[[Java MOC]]"
Related: 
Completed: false
---
---

>[!info] Index
>1. [[#Introduction]]
>2. [[#println()]]
>3. [[#print()]]
>4. [[#printf()]]

---
## Introduction
In Java, to standard output (screen) you can simply use:
- `System.out.println();`
- `System.out.print();`
- `System.out.printf();`

Here:
- `System` is a [[Java Class and Objects|class]]
- `out` is a `public` `static` [[Java Fields|field]]

---
## println() and print()

- `print()` - It prints string inside the quotes.
- `println()` - It prints string inside the quotes similar like `print()` method. Then the cursor moves to the beginning of the next line.

```java
class Output {
    public static void main(String[] args) {
    	
        System.out.println("1. println ");
        System.out.println("2. println ");
    	System.out.println();
    	
        System.out.print("1. print ");
        System.out.print("2. print");
    }
}
```

Output:
```text
1. println 
2. println 

1. print 2. print
```

**It can be used to print variables:**

```java
int x = 5;
int y = 6;
System.out.println(x + y); // Print the value of x + y


String firstName = "John ";
String lastName = "Doe";
String fullName = firstName + lastName;
System.out.println(fullName);


```

---
## printf()



---