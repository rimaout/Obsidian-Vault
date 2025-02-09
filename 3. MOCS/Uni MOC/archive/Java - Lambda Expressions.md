---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: true
created: 2025-02-02T00:07
updated: 2025-02-02T21:07
---
>[!danger] TLDR
>
>Una lambda function è una tecnica per definire una funzione in modo compatto. È stata introdotta nella versione 8 di Java come parte delle funzionalità di programmazione funzionale.
>
>Le lambda function creano oggetti anonimi assegnabili a riferimenti di interfacce funzionali. 
>
>**oss:** *Funzione anonima* è oggetto virtuale non istanziato nella heap.

## Introduzione

Una lambda function è una funzione che non ha un nome e che può essere definita utilizzando la sintassi seguente:

```java
(parametri) -> { corpo della funzione }
```

Dove:
- `(parametri)` è la lista dei parametri della funzione, separati da virgole.
- `->` è l'operatore di lambda, che separa la lista dei parametri dal corpo della funzione.
- `{ corpo della funzione }` è il corpo della funzione, che può contenere una o più istruzioni e l'eventuale output

Le lambda function possono essere utilizzate in diversi modi, ad esempio:

- Come argomento di un metodo che accetta un'interfaccia funzionale come parametro.
- Come valore di ritorno di un metodo.
- Come membro di una collezione.

>[!note] Memoria Lambda Function
>
>Il `this` si riferisce all oggetto della classe esterna in cui è usata, vengono compilate come dei metodi privati e quindi non vanno nella heap.
>
>***Differenza con*** [[Java - Anonymous Classes]]

## Interfacce Funzionali e Lambda function

Le lambda function possono essere utilizzate per implementare le [[Java - SAM & Functional Interfaces]], dove la funzione lambda deve rispettare i parametri in input e il tipo in output dell'unico metodo astratto dell'interfaccia funzionale.

```java
@FunctionalInterface 
interface FunzioneMatematica {     
	int calcola(int x, int y); 
} 
```

```java
FunzioneMatematica somma = (int x, int y) -> {return x + y;};
FunzioneMatematica prodotto = (int x, int y) -> {return x * y;};

System.out.println(somma.calcola(2, 5)); // output: 7
System.out.println(somma.calcola(2, 5)); // output: 10
```

>[!note] Tipi generici
>
>Le lambda function posso implementare anche interfacce funzionali con tipi generici:
>
>```java
>@FunctionalInterface 
>interface Converter<F, T> {     
>	T convert(F from); 
>}
>
>//Main
>Converter<String, Integer> intConverter = from -> Integer.valueOf(from);
>Converter<String, MyString> stringConverter = a -> new MyString(a)
>```

## Vantaggi Limiti

Le lambda function offrono diversi vantaggi, tra cui:

- Sintassi più concisa rispetto alle classi anonime.
- Possibilità di definire funzioni in linea all'interno di un codice.
- Miglioramento della leggibilità del codice.

Tuttavia, le lambda function hanno anche alcuni limiti, tra cui:

- Non possono essere utilizzate per implementare interfacce con più di un metodo astratto.
- Non possono essere utilizzate per definire costruttori o metodi statici.
- Non possono essere utilizzate per accedere a variabili non finali dell'ambiente circostante.

## Versione Compatta

Esistono delle sintassi semplificate per le lambda functions:

- Se si implementa un interfaccia funzionale non serve specificare i tipi in input, essendo già definiti nell'interfaccia.
- Se il corpo della funzione è una singola istruzione possiamo omettere le parentesi graffe.
- Se si restituisce un singolo valore possiamo omettere il `return`.
- Se in input abbiamo un singolo parametri possiamo omettere le parentesi tonde.



