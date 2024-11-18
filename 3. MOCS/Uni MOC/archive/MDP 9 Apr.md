---
created: 2024-04-09
type: Uni Note
class:
  - "[[Metodologie di Programmazione (class)]]"
academic year: 2023/2024
related: 
completed: false
updated: 2024-05-27T13:29
---
---

>[!info] Index
>1. 

---
## Interfacce notevoli

![[Pasted image 20240409092733.png|600]]

Sono classi notevoli anche `Iterator`

>[!warning] oss
>Clonable non crea una deep copy ma solo una shallow copy [[Python Alias, Shallow and Deep copy]]

**Altra interfaccia utile:**

##### Interfaccia Runnable
interfaccia che implementa un solo metodo `run()` che permette di creare thread che permette di eseguire un metodo in modo separato dal resto del programma 

```java
public interface Runnable{
	void run()
}
```

---
## Le enumerazioni possono estendere le interfacce 

![[Pasted image 20240409094039.png|800]]

---
## metodo clone()
`clone()` appartiene all'interfaccia `cloneable` e permette di fare una shallow copy di un oggetto, questo significa che quando l’oggetto ha come capi dei riferimenti (puntatori) crea dei problemi (ovvero non viene effettuata la creazione di un nuovo riferimento, quindi i riferimenti dell’oggetto originale e della copia punteranno allo stesso riferimento )

>[!warning] oss
>`x.clone() != x` sarà sempre vero 

>[!danger] Utilizzo
>`clone()` per esse utilizzati deve essere implementato oppure verrà ritornato l'errore `CloneNotSupportedException`

##### Sovrascrivere `clone()`


---
## Classi top level 
- Non sono contenute in altre classi
- Questo tipo di classi richiede un file .java dedicato con lo stesso nome della classe che esso contiene

---
## Classic annidate (nested class)
- classi all’interno di altre classi

**Esistono 2 tipi:**
- `static`
- `non-static` in questo caso vengono dette classi interne (inner class)

- Prima di poter creare un oggetto della classe interna è necessario istanziare la classe esterna (top-level) che la contiene
- Ciascuna classe interna, infatti, ha un riferimento implicito all’oggetto della classe che la contiene
- Dalla classe interna è possibile accedere a tutte le variabili e a tutti i metodi della classe esterna
- Come tutti i membri di una classe, le classi interne possono essere dichiarate public, protected o private

**Esempio:**
![[Pasted image 20240409103616.png|900]]

---
## Static nested class

![[Pasted image 20240409104358.png|600]]

---
## Classi anonime
- classi senza nome che permettono di implementare un interfaccia o di estendere una classe

**Syntax:**
```java
TipoDaEstendere unicoRiferimentoOggetto = new TipoDaEstendere(){
	//codice della classe anonima
};
```

**Esempio:**
![[Pasted image 20240409110640.png|400]]

---
## Interfacce funzionali
- In Java 8 è disponibile una nuova annotazione `@FunctionalInterface`
- L’annotazione garantisce che l’interfaccia sia dotata esattamente di un solo metodo astratto

**Esempio:**
```java
@functionalInterface
public interface Runnable{
	void run();
}
```

---
## Espressioni Lambda

- Presenti da java 8
- Tali espressioni creano oggetti anonimi assegnabili a riferimenti a interfacce funzionali compatibili con l’intestazione (input/output) della funzione creata.

**Syntax:**

```java
(parameters) -> { code block }
```

>[!tip]
>- Il tipo dei parametri si può omettere
>- return si può omettere 
>- se c'e un solo parametro in input si possono omettere le tonde
>- le graffe si possono omettere solo se il cose block è du una sola riga

![[Pasted image 20240409112642.png|400]]

**How to make and run a lambda object:**
```java
Runnable obName = (parameters)  -> { code block };
obName.run(input);
```

Example:
```java
Runnable r = () -> { System.out.println(ʺhello, lambda!ʺ); };
r.run(); // stampa ʺhello, lambda!ʺ
```

**It can be used in a for**

```java
 ArrayList<Integer> numbers = new ArrayList<Integer>();
    numbers.add(5);
    numbers.add(9);
    numbers.add(8);
    numbers.add(1);
    numbers.forEach( (n) -> { System.out.println(n); } );
```

**Altri esempi:**
![[Pasted image 20240409112842.png|500]]

---
