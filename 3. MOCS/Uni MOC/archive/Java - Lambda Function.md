---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: false
created: 2025-02-02T00:07
updated: 2025-02-02T00:19
---
Una lambda function in Java è un tipo di funzione anonima che può essere definita in linea all'interno di un codice. È stata introdotta nella versione 8 di Java come parte delle funzionalità di programmazione funzionale.

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

Esempio `(x, y) -> {x + y}`<

## Interfaccie Funzionali e Lambda function

Le interfaccie funzionali sono un tipo di interfaccia che contiene un solo metodo astratto. Le lambda function possono essere utilizzate per implementare queste interfacce.

Ecco un esempio di come utilizzare una lambda function per implementare un'interfaccia funzionale:


```java

@FunctionalInterface 
interface Somma {     
	int somma(int x, int y); 
} 

public class Main {     
	public static void main(String[] args) {         
		Somma somma = (x, y) -> x + y;         
        System.out.println(somma.somma(2, 3)); // stampa 5     
    } 
}
```
In questo esempio, la lambda function `(x, y) -> x + y` è utilizzata per implementare l'interfaccia funzionale `Somma`. La lambda function prende due parametri `x` e `y` e restituisce la loro somma.

## Vantaggi Limiti

Le lambda function offrono diversi vantaggi, tra cui:

- Sintassi più concisa rispetto alle classi anonime.
- Possibilità di definire funzioni in linea all'interno di un codice.
- Miglioramento della leggibilità del codice.

Tuttavia, le lambda function hanno anche alcuni limiti, tra cui:

- Non possono essere utilizzate per implementare interfacce con più di un metodo astratto.
- Non possono essere utilizzate per definire costruttori o metodi statici.
- Non possono essere utilizzate per accedere a variabili non finali dell'ambiente circostante.