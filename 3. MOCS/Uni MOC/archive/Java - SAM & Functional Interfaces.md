---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: true
created: 2025-01-30T18:35
updated: 2025-01-31T16:34
---
## SAM (Single Abstract Method)

Una SAM è un'interfaccia che contiene un solo metodo astratto, ovvero un metodo che non ha un'implementazione

```java
public interface MySAM {     
	void doSomething();
}
```

>**Osservazione:** ogni SAM è anche un'interfaccia funzionale, ma non ogni interfaccia funzionale è necessariamente una SAM

## Functional Interfaces

Un'interfaccia funzionale, invece, è un'interfaccia che contiene un solo metodo astratto e può avere degli opzionali metodi default.

```java
public interface MyFunctionalInterface {
    void doSomething();

    default void doSomethingElse() {
        System.out.println("Doing something else");
    }
}
```
