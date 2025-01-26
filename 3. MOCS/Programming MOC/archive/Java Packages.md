---
created: 2024-03-12
type: Programming Note
programming language: "[[Java MOC]]"
related: 
completed: false
updated: 2025-01-25T19:40
---
---

>[!info] Index
>1. [[#Introduction]]
>2. [[#Built-in Package]]
>
>- [[Java Import a Package]]
>- [[Java Create a Package]]

---
## Introduction

A package is simply a container that groups related types (Java classes, interfaces, enumerations, and annotations

---
## Built-in Package

Built-in packages are existing java packages that come along with the [JDK](https://www.programiz.com/java-programming/jvm-jre-jdk#jdk). 

For example, `java.lang`, `java.util`, `java.io`, etc. For example:

```java
import java.util.ArrayList;

class ArrayListUtilization {
    public static void main(String[] args) {

        ArrayList<Integer> myList = new ArrayList<>(3);
        myList.add(3);
        myList.add(2);
        myList.add(1);

        System.out.println(myList);
    }
}
```

>[!warning] oss
>You don't need to import `java.lang` because it’s already integrated with the java environment