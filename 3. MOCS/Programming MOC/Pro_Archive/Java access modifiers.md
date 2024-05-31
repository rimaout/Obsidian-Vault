---
created: 2024-03-13
type: Programming Note
programming language: "[[Java MOC]]"
related:
  - "[[Java OOP]]"
completed: true
updated: 2024-05-27T13:29
---
---

>[!info] Index
>1. [[#Overview]]
>2. [[#Default]]
>3. [[#Public]]
>4. [[#Private]]
>5. [[#Protected]]

---
## Overview

In this tutorial, we’re going over access modifiers in Java, which are used for setting the access level to [[Java Class and Objects|classes]], [[Java Variables|variables]], [[Java Methods|methods]], and [[Java Constructor|constructors]].

**There are four access modifiers:** 
- [[#Default]] (no keyword)
- [[#Public]]
- [[#Private]]
- [[#Protected]]

The table below summarises the available access modifiers:

| Modifier  | Class | Package | Subclass | World |
| --------- | ----- | ------- | -------- | ----- |
| public    | Y     | Y       | Y        | Y     |
| protected | Y     | Y       | Y        | N     |
| default   | Y     | Y       | N        | N     |
| private   | Y     | N       | N        | N     |

>[!warning] oss
>We can see that a class, regardless of the access modifiers used, always has access to its members:

---
### Default 

When we don’t use any keyword explicitly, Java will set a **default** access to a given class, method or property.

The default access modifier is also called _package-private_, which means that **all members are visible within the same package** but aren’t accessible from other packages.

---
### Public

If we add the _public_ keyword to a class, method or property then **all other classes in all packages will be able to use it**. 

>[!warning] oss
This is the least restrictive access modifier.

---
### Private

Any method, property or constructor with the _private_ keyword **is accessible from the same class only**. 

>[!warning] oss
>This is the most restrictive access modifier and is core to the concept of encapsulation. All data will be hidden from the outside world:

---
### Protected

Between [[#Public]] and [[#Private]] access levels, there’s the protected access modifier.

If we declare a method, property or constructor with the _protected_ keyword, we can access the member from the **same package** (as with _package-private_ access level) and in addition from **all subclasses of its class**, even if they lie in other packages:

```java
package com.baeldung.accessmodifiers;

public class SuperPublic {
    static protected void protectedMethod() {
        ...
    }
}
```

_protectedMethod()_ is available in subclasses (regardless of the package):

```java
package com.baeldung.accessmodifiers.another;

import com.baeldung.accessmodifiers.SuperPublic;

public class AnotherSubClass extends SuperPublic {
    public AnotherSubClass() {
        SuperPublic.protectedMethod(); // Available in subclass. Let's note different package.
    }
}
```

---