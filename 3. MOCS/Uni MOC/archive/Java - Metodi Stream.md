---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: false
created: 2025-02-08T17:53
updated: 2025-02-09T20:09
---
#### Min e Max

`min(comparator)` e `max(comparator)` restituiscono il minimo e il massimo di uno stream confrontando in base al [[Java - Notable Interfaces#Comparable e Comparator|comparator]] passato.

```java
// Esempi
Integer min = stream.min(Integer::compare)
Integer max = stream.max(Integer::compare)
Integer min = stream.min((a, b) -> a.compareTo(b)
```

#### Filter

`filter(predicate)` restituisce un nuovo stream con i soli elementi che rispettano il [[Java - Notable Functional Interfaces#Predicate|predicate]] dato. 

```java
Stream<String> stream2 = Stream.of("apple", "banana", "cherry", "avocado"); 
stream2.filter(s -> s.startsWith("a"))

Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 10, 20, 30); 
stream.filter(n -> n > 10)
```

#### ForEach

Prende in input un [[Java - Notable Functional Interfaces#Consumer|consumer]] e lo applica a tutti gli elementi dello stream.

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 10, 20, 30); 
stream.forEach(System.out::println);
```

#### Count 

Restituisce un long che rappresenta il numero di elementi dello stream

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5); 
long count = stream.count();
```

#### Sorted

Restituisce uno stream ordinato secondo l'ordinamento naturale degli elementi o è possibile passare un [[Java - Notable Interfaces#Comparable e Comparator|comparator]].

```java
// Ordina gli elementi di uno stream di oggetti Persona in base all'età 

Stream<Persona> stream = Stream.of( 
	new Persona("Mario", 30), 
	new Persona("Luigi",25), 
	new Persona("Giovanni", 40) 
); 
stream.sorted((p1, p2) -> Integer.compare(p1.getEta(p2.getEta())));
```

#### Map

Restituisce un nuovo stream dove ciascun elemento è stato convertito tramite la *funzione* passata in input.

```java
Stream<Integer> stream = Stream.of(5, 2, 8, 1, 9, 15, 20); 
stream.map(n -> n * 2)

// Trasforma gli elementi di uno stream di stringhe in un nuovo tipo di dati e poi appiattisce il risultato 
Stream<String> stream = Stream.of("1,2,3", "4,5,6"); 
stream.map(s -> s.split(",")).flatMap(Arrays::stream).forEach(System.out::println);
```

#### Collect

Raccogli gli elementi di uno stream in un oggetto (Array, String, Lista,  Set...) e lo restituisce come risultato.

>Collect è uno strumento molto potente vedi la sezione [[Java - Collectors]] per approfondire.

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5); 

// Raccogli in una lista di interi
List<Integer> lista = stream.collect(Collectors.toList());
// Raccogli in una array di interi
Integer[] array = stream3.collect(Collectors.toArray(Integer[]::new)); 
```

#### Distinct

Restituisce un nuovo stream ma senza ripetizioni

```java
// Rimuove gli elementi duplicati da uno stream di numeri interi 
Stream<Integer> stream = Stream.of(1, 2, 2, 3, 3, 3, 4, 5, 5); 
stream.distinct().forEach(System.out::println);
```

#### Reduce

Applica una funzione di riduzione a tutti gli elementi dello stream, riducendoli a un singolo valore.

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5); 
int somma = stream.reduce((a, b) -> a + b)
```

#### Limit

Metodo che prende in input un long `n` e restituisce uno stream che contiene solo i primi `n` elementi dello stream originale.

```java
Stream<String> stream = Stream.of("1", "2", "3", "4", "5"); 
Stream<String> limitStream = stream.limit(3);
```

#### Skip

Metodo che prende in input un long `n` e restituisce uno stream che salta i primi `n` elementi dello stream originale e contiene solo gli elementi rimanenti.

```java
Stream<String> stream = Stream.of("1", "2", "3", "4", "5"); 
Stream<String> limitStream = stream.skip(3);
```

#### TakeWhile e DropWhile

**takeWhile**: restituisce uno stream che contiene tutti gli elementi dello stream originale fino a quando la condizione specificata (predicate) non viene violata.

**dropWhile**: restituisce uno stream che salta tutti gli elementi dello stream originale fino a quando la condizione specificata (predicate) non viene violata.

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9); 

Stream<Integer> takeWhileStream = stream.takeWhile(n -> n <= 5);
Stream<Integer> dropWhileStream = stream.dropWhile(n -> n <= 5);
```

#### AnyMatch, AllMatch e NonoMatch

**anyMatch**: restituisce `true` se almeno un elemento dello stream soddisfa la condizione specificata ([[Java - Notable Functional Interfaces#Predicate|predicate]]), `false` altrimenti.

**allMatch**: restituisce `true` se tutti gli elementi dello stream soddisfano la condizione specificata ([[Java - Notable Functional Interfaces#Predicate|predicate]]), `false` altrimenti.

**noneMatch**: restituisce `true` se nessun elemento dello stream soddisfa la condizione specificata ([[Java - Notable Functional Interfaces#Predicate|predicate]]), `false` altrimenti.

```java
Stream<Integer> stream = Stream.of(6, 7, 8, 9); 

boolean result = stream.allMatch(n -> n > 5);
boolean result = stream.noneMatch(n -> n > 5);
boolean result = stream.anyMatch(n -> n > 5);
```

#### FindFirst e FindAny

**findFirst**: restituisce il *primo elemento* dello stream che *soddisfa la condizione specificata* ([[Java - Notable Functional Interfaces#Predicate|predicate]]), o un `Optional` vuoto se nessun elemento soddisfa la condizione.

**findAny**: restituisce un *elemento qualsiasi* dello stream che *soddisfa la condizione specificata* ([[Java - Notable Functional Interfaces#Predicate|predicate]]), o un `Optional` vuoto se nessun elemento soddisfa la condizione.

#### FlatMap

Se abbiamo uno stream di array ed usiamo:
- `.map(Arrays::stream)`  otteniamo uno stream di stream
- `.flatMap(Array::stream)` otteniamo un stream

