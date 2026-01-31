---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: false
created: 2025-02-08T18:07
updated: 2026-01-31T13:32
---
#### Function

L'interfaccia funzionale `Function<T, R>` in Java è un'interfaccia funzionale che rappresenta una funzione che accetta un argomento di tipo `T` e restituisce un valore di tipo `R`.

Contiene un metodo **apply**: `R apply(T t)`

```java
Function<Integer, Integer> quadrifica = x -> x * x; 
int risultato = quadrifica.apply(5); 
System.out.println(risultato); // stampa 25
```

>[!note] Metodi di default
>
>- `andThen(funzione)`: ritorna una funzione composta, che effettua prima la funzione su cui lo invochiamo e poi la funzione che abbiamo passato in input.
>- `copose(funzione)`: ritorna una funzione composta dove viene prima effettuata la funzione in input e poi quella su cui è chiamato il metodo.
>- `identify()`: ritorna la funzione identità che ritorna sempre il suo parametro.
>  
>```java
>Function`<Integer, Integer> quadrifica = x -> x * x; 
>Function`<Integer, Integer> triplica = x -> x * 3; 
>Function`<Integer, Integer> composizione = quadrifica.andThen(triplica); 
>
>int risultato = composizione.apply(5); 
>System.out.println(risultato); // stampa 75
>```

#### Predicate

L'interfaccia `Predicate<T>` in Java è un'interfaccia funzionale che rappresenta una funzione che accetta un argomento di tipo `T` e restituisce un valore booleano.

Contiene il metodo **test**: `boolean test(T t)`

```java
Predicate<Integer> maggioreDi10 = x -> x > 10; 
boolean risultato =` maggioreDi10.test(15); 
System.out.println(risultato); // stampa true
```

>[!note] Metodi di default
>- `and(Predicate<? super T> other)`: ritorna una funzione composta che effettua prima la funzione su cui lo invochiamo e poi la funzione che abbiamo passato in input. La funzione composta restituisce `true` solo se entrambe le funzioni restituiscono `true`.
>- `or(Predicate<? super T> other)`: ritorna una funzione composta che effettua prima la funzione su cui lo invochiamo e poi la funzione che abbiamo passato in input. La funzione composta restituisce `true` se almeno una delle funzioni restituisce `true`.
>- `negate()`: ritorna una funzione che nega la funzione originale. La funzione negata restituisce `true` se la funzione originale restituisce `false`, e `false` altrimenti.
>  
>  ```java
>  Predicate`<Integer> maggioreDi10 = x -> x > 10; 
>Predicate`<Integer> minoreDi20 = x -> x < 20; 
>
>Predicate`<Integer> compresoTra10E20 = maggioreDi10.and(minoreDi20);
>``` 

#### Supplier

L'interfaccia `Supplier<T>` in Java è un'interfaccia funzionale che rappresenta una funzione che non accetta argomenti e restituisce un valore di tipo `T`.

>**oss:** spesso utilizzato con i costruttori che non hanno input

```java
Supplier<Integer> numeroCasuale = () -> (int) (Math.random() * 100); 
int risultato = numeroCasuale.get(); 
System.out.println(risultato); // stampa un numero casuale
```

#### Consumer

L'interfaccia `Consumer<T>` in Java è un'interfaccia funzionale che rappresenta una funzione che accetta un argomento di tipo `T` e non restituisce alcun valore.

```java
void accept(T t);
```

L'interfaccia `Consumer` ha un solo metodo astratto, chiamato `accept`, che viene utilizzato per eseguire l'azione sulla classe di tipo `T`.

```java
Consumer<String> stampaMessaggio = messaggio -> System.out.println(messaggio); 
stampaMessaggio.accept("Ciao, mondo!");
```