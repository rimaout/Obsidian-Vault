---
created: 2024-02-28
type: Programming Note
programming language: "[[Java MOC]]"
related: 
completed: true
updated: 2024-05-27T13:29
---
---

>[!info] Index:
>1. [[#Java "Hello, World!" Program]]
>2. [[#How does it work?]]
>3. [[#Running the program]]

---
## Java "Hello, World!" Program

```java
// Your First Program

class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!"); 
    }
}
```

```
Output: Hello, World!
```

## How does it work?
1. `// Your First Program`
	 - In Java, any line starting with `//` is a comment. 

3. `class HelloWorld { ... }`  
    - In Java, every application begins with a class definition. In the program, HelloWorld is the name of the class.

	- For now, just remember that every Java application has a class definition, and the name of the class should match the filename in Java.

3. `public static void main(String[] args) { ... }`  
      
    - This is the main method. Every application in Java must contain the main method. The Java compiler starts executing the code from the main method.  
      
    - For now, just remember that the main function is the entry point of your Java application, and it's mandatory in a Java program.
    
4. `System.out.println("Hello, World!");`  
    - The code above is a print statement. It prints the text `Hello, World!` to standard output (your screen). The text inside the quotation marks is called [[Java Strings]].
    
    - Notice the print statement is inside the main function, which is inside the class definition.

## Running the program

![[Pasted image 20240229123207.png|600]]

---