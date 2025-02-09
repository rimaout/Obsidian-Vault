---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: true
created: 2025-01-30T18:35
updated: 2025-02-08T13:17
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

## Come Implementare un Interfaccia funzionale


In generale, le ***lambda expression*** e i ***riferimenti a metodo*** sono i modi più concisi e leggibili per implementare le interfacce funzionali, mentre le ***classi anonime*** e le ***implementazioni esplicite*** possono essere utili in situazioni più complesse

**1. Implementazione esplicita:**

```java
public class saluta implements Consumer<Persona> {
    @Override
    public void accept(Persona p) {
        System.out.println("Ciao " + p.nome);
    }
}

Saluta saluta = new Saluta();

// Salutare una persona:
saluta.accept(new Persona("Giovanni", "Verdi"))

// Salutare tutte le presone dentro una lista:
List<Persona> persone = new ArrayList<>();
persone.forEach(saluta);
```

**2. Implementazione con lambda expression:**

```java
Consumer<Persona> saluta = p -> System.out.println("Ciao " + p.nome);

// Salutare una persona:
saluta.accept(new Persona("Giovanni", "Verdi"))

// Salutare tutte le presone dentro una lista:
List<Persona> persone = new ArrayList<>();
persone.forEach(saluta);
```

**3. Implementazione con riferimento a metodo:**

```java
Consumer<Persona> saluta = System.out::println 

// Print una persona:
saluta.accept(new Persona("Giovanni", "Verdi"));
  
// Print di tutte le persone dentro una lista: 
List<Persona> persone = new ArrayList<>();
persone.forEach(saluta);
```

In questo caso si farà il print della persona infatti *non è possibile modificare il metodo* per far salutare il nome della persona.

**4. Implementazione con classe anonima:**

```java
Consumer<Persona> saluta = new Consumer<Persona>() {
    @Override
    public void accept(Persona p) {
        System.out.println("Ciao " + p.nome);
    }
});

// Salutare una persona:
saluta.accept(new Persona("Giovanni", "Verdi"))

// Salutare tutte le presone dentro una lista:
List<Persona> persone = new ArrayList<>();
persone.forEach(saluta);
```
