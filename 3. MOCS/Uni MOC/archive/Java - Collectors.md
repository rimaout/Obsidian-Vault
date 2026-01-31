---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: false
created: 2025-02-09T20:09
updated: 2026-01-31T13:32
---
Sono oggetti in grado di ridurre il numero di elementi dello stream e/o di collezionali all'interno di una struttura dati.

**Metodi che riducono ad un solo numero:** `counting`, `maxBy`, `summingInt`, `averageInt`.

**Metodi che trasformano lo stream in una struttura dati:**  `toList` o `toSet` trasformano in una list o set senza però nessuna garanzia sul tipo specifico di quest'ultimi.

#### toCollection

Accumula gli elementi dello steam in una collezione scelta, passando al metodo il costruttore della collezione

```java
ArrayList<String> str = l.stream().map(x -> x+" ").collect(toCollection(ArrayList::new))
```

#### toMap

Metodo che permette di trasformare uno stream in una mappa, trasformando ogni elementi dello stream in una coppia chiave valore.

Richiede richiede 2, 3 o 4 parametri:
1. [[Java - Notable Functional Interfaces#Function|Function]] per determinare la chiave
2. [[Java - Notable Functional Interfaces#Function|Function]] per determinare il valore
3. [[Java - Notable Functional Interfaces#Function|Function]] (opzionale) per determinare cosa fare quando sono presenti più elementi con la stessa chiave 
4. [[Java - Notable Functional Interfaces#Supplier|Supplier]] (opzionale) con cui è possibile indicare il costruttore della mappa che si vuole utilizzare (`HashMap::new`, `TreMap::New` e `LinkedHashMap::new`)

```Java
ArrayList<Person> people = new ArrayList<Person>()

Map<Integer, String> map = people.stream()
.collect(Collectors.toMao(
	Person::getName;
	Person::getAge;
	(n1, n2) -> n1 + "; " + n2 // come chiave avremmo il nome delle due persone divise da punto e virgola
	HashMap::new
));
```

#### gropingBy

Il metodo `groupingBy` accetta un parametro di tipo `Function` che specifica la proprietà in base alla quale gli elementi devono essere raggruppati. Il risultato è un `Map` dove la key è il valore della proprietà specificata e la value è una lista di elementi che hanno quella proprietà.

```java
ArrayList<Person> people = new ArrayList<Person>()
Map<City, List<person>> peopleByCity = people.stream().collect(groupingBy(Person::getCity))
```

#### mapping

Il metodo `mapping()` prende in input 
- una [[Java - Notable Functional Interfaces#Function|Funzione]] che viene utilizzata su gli elementi dello stream e poi viene generato una collezione contenente i nuovi elementi.
- un **collector** per specificare la collezione da utilizzare (es. `toSet()`)

```java
ArrayList<Person> people = new ArrayList<Person>()
Set<String> NomiPersone = people.stream().collect(Collectors.mapping(Person::getName, toSet()));
```

#### partitioningBy

Il metodo `partitioningBy()` prende in input un [[Java - Notable Functional Interfaces#Predicate|predicate]] e crea una mappa con due chiave `True` e `False`:
- Il valore delle chiave `true` è la lista di elementi che rispettano il predicate
- Il valore delle chiave `false` è la lista di elementi che non rispettano il predicate

```java
ArrayList<Person> people = new ArrayList<Person>();  
Map<Boolean, List<Person>> teenagers = people.stream().collect(Collectors.partitioningBy(p -> p.getAge() <= 19));
```