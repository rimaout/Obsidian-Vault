---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: false
created: 2025-02-09T20:09
updated: 2025-02-10T17:23
---
Sono oggetti in grado di ridurre il numero di elementi dello stream, oppure anche collezionati all'interno di una struttura dati.

Infatti troviamo alcuni metodi come counting, maxBy, summingInt, averaginhInt che riducono il nostro stream in un solo numero.

Oppure altri metodi che trasformano il nostro stream in una struttura dati toList o toSet lo trasformano in una list o un setsenza però nessuna garanzia sul tipo specifico di quest'ultimi.

#### toCollection

Accumula gli elementi dello steam in una collezione scelta, passando al metodo il costruttore della collezione

```java
ArrayList<String> str = l.stream().map(x -> x+" ").collect(toCollection(ArrayList::new))
```

#### toMap



#### gropingBy

Il metodo `groupingBy` accetta un parametro di tipo `Function` che specifica la proprietà in base alla quale gli elementi devono essere raggruppati. Il risultato è un `Map` dove la chiave è il valore della proprietà specificata e il valore è una lista di elementi che hanno quella proprietà.

```java
Map<City, List<person>> peopleByCity = people.stream().collect(groupingBy(Person::getCity))
```

#### mapping



#### partitioningBy