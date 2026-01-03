---
type: Programming Note
programming language: "[[Java MOC]]"
related:
  - "[[Metodologie di Programmazione (class)]]"
completed: false
created: 2024-06-17T18:21
updated: 2025-02-11T12:49
---
## Introduzione 

Un `Stream` in Java può essere visto come una sequenza di dati proveniente da una sorgente (ad esempio una [[Java - Collections|collezione]] o [[Java - Arrays|array]]), su cui possiamo effettuare delle operazioni.

## Tipi di Operazioni

>[!note] Operazioni Intermedie vs Terminali
>Le operazioni **intermedie** restituiscono un altro stream su cui continuare a lavorare.
>- ad esempio: `map()`, `filter()`, `sorted()` 
>
>Le operazioni **terminali** restituisco un tipo atteso e terminano lo stream impedendone il riutilizzo.
>- ad esempio: `collet()`, `sorted()`

>[!note] Operazione State-less vs State-full
>
>Le operazioni **state-less** vengono elaborate in modo indipendente tra gli elementi, questo significa che possono essere parallelizzate.
>- ad esempio: `filter()`
>
>Le operazioni **state-full** sono operazioni dove l'elaborazione di un elemento potrebbe dipendere da un altro elemento, e che quindi non possono essere parallelizzate.
>- ad esempio: `sorted()`

>[!warning] Lazy Behaviour
>
>Le operazione intermedie non vengono eseguite immediatamente ma soltanto nel momento quando viene effettuata un operazione terminale.
>
>Quest'approccio permette di ottimizzare il consumo di memoria e migliorare le prestazioni.

## Tipi di Stream

>[!note] Stream Sequenziali vs Paralleli
>Un stream sequenziale ha un unico elemento corrente, elaborato in modo indipendente dagli altri. 
>
>Un stream parallelo è in grado di suddividere il suo lavoro in più parti, elaborando più elementi contemporaneamente.

>[!note] Stream Primitivi
>
>Gli stream normalmente possono lavorare solo su oggetti, per questo sono stati creati degli stream speciali soltanto per i primitivi, che non richiedono di passare attraverso le classi [[Java - Wrapper Classes, Auto-boxing and Auto-unboxing#Classi Wrapper|classi wrapper]].
>
>Ad esempio `IntStream`, `DoubleStream` e `LongStream`

## Come Creare uno stream

Per creare uno stream ci sono diversi modi:

Utilizzare `Stream.of(elenco dati)` 

```java
Stream.of(1,2,3,4)
Stream.of(new Persona("Mario"), new Persona "Giulia"))
```

Utilizzare il metodo `stream()` o `parallelStream()` delle collection:

```java
List<Persona> persone = new ArrayList<>();
persone.stream();
persone.stream();
```

É possibile creare uno stream da un array utilizzare il metodo `Array.stream(T[] array)`

```java
Integer[] numeri = {1, 2, 3, 4, 5}; 
Arrays.stream(numeri);
```

Uno stream di righe di testo da `BufferedReader.lines()`, `Files.lines(path)` e `String.lines()`

```java
BufferedReader reader = new BufferedReader(new FileReader("file.txt")); 
reader.lines() // lines è uno stream

Files.lines("file.txt") // lines è uno stream

String testo = "Linea 1\n Linea 2\n Linea 3";
testo.lines() // lines è uno stream
```

## Stream Infiniti

È possibile creare degli stream infiniti attraverso il metodo `iterate` che prende in input un valore iniziale e una funzione da allocare al valore iniziale per calcolare i successivi.

```java
Stream<Integer> numeri = Stream.iterare(0, n -> n+10);
numeri.limit(5).forEach(System.out::println); // 0, 10, 20, 30, 40
```

