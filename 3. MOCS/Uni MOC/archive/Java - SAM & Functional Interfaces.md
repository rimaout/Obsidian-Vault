---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: false
created: 2025-01-30T18:35
updated: 2025-01-30T18:40
---
## SAM (Single Abstract Method)


```java
public interface MySAM {     
	void doSomething();
}
```

```java
public interface MyFunctionalInterface {
    void doSomething();

    default void doSomethingElse() {
        System.out.println("Doing something else");
    }
}
```