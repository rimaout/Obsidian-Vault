---
created: 2024-05-14
type: Uni Note
class:
  - "[[Introduzione agli Algoritmi (class)]]"
academic year: 2023/2024
related: 
completed: false
updated: 2024-05-27T13:29
---
---

>[!abstract] Index
>1. 

>[!abstract] Related
>- 

---

## Optional 
`java.util.Optional`

Optional è un contenitore che ci permette di specificare che il nostro metodo può tornare Null 

## Stram
Interfaccia `java.utill.stream.Stream` - Rappresenta una sequenza di elementi su cui possono essere effettuate una o più operazioni **sequenziali** e **parallele** 

Uno stream non modifica o memorizza i dati della sorgente ma opera su essi

Le operazioni possono essere:
- **Intermedie:** restituiscono un altro stream su ui continuare a lavorare
- **Terminali:** restituiscono il tipo atteso

Su uno stream posso dichiarare più operazioni intermedie ma solo un unica (finale) operazione terminale

**lazy behaviour:** Le operazioni intermedie non vengono eseguite immediatamente, m solo quando si richiede l'esecuzione di un operazione terminale

Le operazioni Intermedie possono essere:
- **Stateless (senza stato):** non hanno nessun impatto sull'ordine delle esecuzioni intermedie, l'elaborazione dei vari elementi può procedere in modo indipendente (es. filter)

- **Stateful (senza stato):** l'elaborazione di un elemento potrebbe dipendere da quella di altri elementi (es. sorted)

##### Stram su primitivi
Steam di base opera su oggetti, ma esistono anche versioni analoghe per 3 tipi primitivi:
- `intStream`
- `DoubleStream`
- `LongStream`

**oss:** Tutte queste interfacce estendono l'interfaccia di base BaseStream

##### Come ottenere uno Stream
- **Direttamente dai dati:** con il metodo statico generico `Stream.of` (elenco di dati di un certo tipo)
- `default Stream<E> stream()` – restituisce un nuovo stream sequenziale
- `default Stream<E> parallelStream()` – restituisce un nuovo stream parallelo, se possibile (altrimenti restituisce uno stream sequenziale)
- E' possibile ottenere uno stream anche per un array, con il metodo statico `Stream<T> Arrays.stream(T[ ] array)`
- E' possibile ottenere uno stream di righe di testo da `BufferedReader.lines()` oppure da `Files.lines(Path)`
- E’ possibile ottenere uno stream di righe anche da `String.lines`

##### Dichiarativi vs Iterativo

- Lo stream permette di utilizzar uno stile **dichiarativo**
- Le collection impone l'utilizzo di uno stile **iterativo**

Lo stream si focalizza sulle operazioni di alto livello da eseguire eventualmente, senza specificare come verranno eseguite 

>[!warning] oss
>Lo Stream è dichiarativo, componibile e parallelizzabile

##### Metodi min e max
 `min` e `max` sono operazioni terminali che:
- Restituiscono rispettivamente il minimo e il massimo di uno stream sotto forma di optional
- Prendono in input un `Comparator` sul tipo degli elementi in input

##### Metodo filter
`filter` è un operazione intermedia che:
- in input accetta un predicato
- in output ritorna lo stream filtrato in base al predicato

##### Metodo forEach
`forEach` è un operazione terminale che:
- Prende in input un Consumer e lo applica a ogni elemento dello stream

##### Metodo count
`count` è un operazione terminale che:
- restituisce il numero di elementi nello stream (l'output è di tipo long)

Esempio:
```java
long startsWithA = l.stream().filter(s -> s.startsWith("a")) .count(); 
System.out.println(startsWithA); // 2
```

```java
//Esempio di conteggio del numero di righe di un file di testo:
long numberOfLines = Files.lines(Paths.get(“yourFile.txt”)).count();
```

##### Metodo sorted

`sorted` è un operazione intermedia che:
- ritorna una visita (copia) ordinata della collezione (senza modificarla)

Esempio:
```java
List<String> l = Arrays.asList("da", "ac", "ab", "bb");

l.stream()  
 .filter(s -> s.startsWith("a")) .forEach(System.out::println);
 .sorted()  
 .forEach(System.out::println);
```

##### Metodo map

`map` è un operazione intermedia che:
- restituisce un nuovo stream in cui ciascun elemento dello stream di origine è convertito in un altro oggetto attraverso la funzione (Function) passata in input

Esempio:
```java
// Restituire tutte le stringhe (portate in maiuscolo) ordinate in ordine inverso
// equivalente a .map(s -> s.toUpperCase()) 
l.stream()
 .map(String::toUpperCase)
 .sorted(Comparator<String>
 .naturalOrder()
 .reversed()) 
 .forEach(System.out::println);
```

##### Metodo collect
`collect` è un operazione terminale che permette di raccogliere gli elementi dello stream in un qualche oggetto

Esempio:
```java
// Ottenere la lista dei prezzi ivati
List<Double> l = ivaEsclusa.stream().map(p -> p*1.22) .collect(Collectors.toList());
```

```java
// Creare una stringa che concatena stringhe in un elenco, rese maiuscole e separate da virgola 
s = l.stream().map(e -> e.toUpperCase()) 
			  .collect(Collectors.joining(", "));
```


## Collectors
`collectors` sono delle "Ricette" per ridurre gli elementi di uno stream e raccoglierli in qualche modo

- **Counting** restituisce il numero di elementi nello stream
- **maxBy/minBy(comparator):** estituisce un Optional con il massimo/minimo valore
- summingInt(lambda che mappa ogni elemento a intero)/averagingInt, summingDouble, averagingDouble
- joining(), joining(separatore), joining(separatore, prefisso, suffisso) – concatena gli elementi stringa dello stream in un'unica stringa finale
- toList, toSet e toMap – accumulano gli elementi in una lista, insieme o mappa (non c'è garanzia sul tipo di List, Set o Map)
- toCollection – accumula gli elementi in una collezione scelta


##### toMap
`toMap` prende in input fino a 4 argomenti:
1. la funzione per mappare l'oggetto dello stream nella chiave della mappa
2. la funzione per mappare l'oggetto dello stream nel valore della mappa
3. *opzionale:* la funzione da utilizzare per unire il valore preesistente nella mappa a fronte della chiave con il valore associato all'oggetto dalla seconda funzione (non devono trovarsi due chiavi uguali o si ottiene un'eccezione `IllegalStateException`)
4. *opzionale:* il Supplier che crea la mappa (fornisce il riferimento )

Esempio:
```java
Map<Integer, String> map = persons 
	.stream()    
    .collect(Collectors.toMap(  
	    Person::getAge,  
	    Person::getName,  
	    (name1, name2) -> name1 + ";" + name2
	)); 
```

##### groupingBy (raggruppamento di elementi)

- groupingBy(lambda che mappa gli elementi di tipo T in bucket rappresentati da oggetti di qualche altro tipo S), restituisce una Map\<S, List\<T\>8\>
- `groupingBy(lambda, downStreamCollector)`, per raggruppamento multilivello

Esempio:
```java
// Ottenere una mappa da città a lista di persone a partire da una lista di persone
Map<City, List<Person>> peopleByCity = xpeople.stream().collect(groupingBy(Person::getCity));
```

```java
// La stessa mappa, ma i cui valori siano insiemi di persone
Map<City, Set<Person>> peopleByCity = people.stream().collect(groupingBy(Person::getCity, toSet()));
```

##### mapping

In raccolte multilivello (per esempio usando groupingBy )è utile mappare il valore del raggruppamento a qualche altro tipo:

```java
Map<City, Set<String>> peopleSurnamesByCity = 
	people.stream().collect(
		groupingBy(Person::getCity, 
			mapping(Person::getLastName, toSet())));
```

## Lezione 16-05-2024

## Creare il proprio stream 


## Partitioning by



## Distinct (inetemedia)
 restituisce uno stream senza ripetizioni di elementi

## Reduce (terminale)

è un operazione terminale che effettua una riduzione sugli elementi dello stream utilizzando la funzione data input
- in input riceve una bi function ovvero una funzione che a un input e un output

Esempio:

senza stream 
```java
int somma = 0;    
    for (int k : lista)
	    somma += k;
```

con stream + reduce:
```java
lista.stream().reduce(0, (a, b) -> a+b); 

// oppure: 
lista.stream().reduce(0, Integer::sum); 
```

## Limit


## takeWhile/dropWhile (intermedie)
- takeWhile: prende elementi a finche si verifica una determinata condizione
- dropWhile: salta elementi finche si verifica la condizione 
 
Esempio:
```java
List<Integer> elementi = List.of(2, 5, 10, 42, 3, 2, 10);  
List<Integer> reduced = l.stream().takeWhile(x -> x < 42).collect(toList()); 
// contiene [2, 5, 10]
```

## anyMatch/allMatch/noneMatch (terminali)


## findFirst e findAny (terminali)


## klaajklsjdkl


## flatMap (intermedia)

- permette di unire più stream in un unico stream

esempio se gli diamo in input una collection di collection, prende tutti gli elementi e li inserisce in un'unica collection


# Lezione 21 May 2023

## IntStream, DoubleStream, LongStream

• Si ottengono da uno Stream con i metodi mapToInt,
mapToLong, mapToDouble
• Analoghi metodi sono disponibili nelle 3 classi (tolto
quello del tipo in questione, es. IntStream non ha
mapToInt), ma in più hanno mapToObj

Dispongono di 2 metodi statici:
– range(inizio, fine), intervallo esclusivo (aperto a destra)
– rangeClosed(inizio, fine), intervallo inclusivo (chiuso a destra)

