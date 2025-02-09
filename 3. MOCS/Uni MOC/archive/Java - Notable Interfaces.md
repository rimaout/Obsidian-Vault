---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: true
created: 2025-01-30T18:05
updated: 2025-02-08T18:00
---
## Iterable e Iterator

In Java, le interfacce `Iterable` e `Iterator` sono due concetti fondamentali per lavorare con collezioni di dati.

>[!note] Iterable
>
>L'interfaccia `Iterable` rappresenta una collezione di oggetti che può essere iterata, ovvero può essere scorsa elemento per elemento. Una classe che implementa `Iterable` deve fornire un metodo `iterator()` che restituisce un oggetto `Iterator` che può essere utilizzato per scorrere la collezione.

>[!note] Iterator
>
>L'interfaccia `Iterator` rappresenta un oggetto che può essere utilizzato per scorrere una collezione di oggetti, che deve fornire tre metodi:
>
>- `hasNext()`: restituisce `true` se ci sono ancora elementi da scorrere, `false` altrimenti.
>- `next()`: restituisce l'elemento successivo nella collezione.
>- `remove()`: rimuove l'elemento corrente dalla collezione (non è obbligatorio implementare questo metodo).

>[!example]- Esempio
>
>```java
>import java.util.Iterator;
>
>public class MiaCollezione implements Iterable<String> {
>    private String[] elementi = {"uno", "due", "tre"};
>
>    @Override
>    public Iterator<String> iterator() {
>        return new MiaIterazione();
>    }
>
>    private class MiaIterazione implements Iterator<String> {
>        private int indice = 0;
>
>        @Override
>        public boolean hasNext() {
>            return indice < elementi.length;
>        }
>
>        @Override
>        public String next() {
>            return elementi[indice++];
>        }
>
>        @Override
>        public void remove() {
>            // non implementato
>        }
>    }
>}
>
>```

## List Iterator

`ListIterator` è un interfaccia che estende l'interfaccia `Iterator` ed è specifica per le liste. Consente di scorrere una lista di oggetti in entrambe le direzioni implementando i metodi:
- `hasNext()`: restituisce `true` se ci sono ancora elementi da scorrere in avanti, `false` altrimenti.
- `hasPrevious()`: restituisce `true` se ci sono ancora elementi da scorrere all'indietro, `false` altrimenti.
- `next()`: restituisce l'elemento successivo nella lista.
- `previous()`: restituisce l'elemento precedente nella lista.
- `remove()`: rimuove l'elemento corrente dalla lista.
- `set(Object o)`: sostituisce l'elemento corrente con l'oggetto specificato.
- `add(Object o)`: aggiunge l'oggetto specificato alla lista.

## Comparable e Comparator

>[!note] Comparable 
>
>`Comparable` è un'interfaccia funzionale che consente di definire un ordinamento per una classe di oggetti. 
>
>Una classe che implementa `Comparable` deve fornire un metodo `compareTo()` che confronta l’oggetto da cui è chiamato con altro oggetto della stessa classe e restituisce:
>- `0` se i due oggetti sono uguali (a livello di ordinamento)
>- `1` se l'oggetto da cui è chiamato è "maggiore" dell'altro oggetto
>- `-1` se l'oggetto da cui è chiamato è "minore" dell'altro oggetto

>[!note] Comparator
>
>`Comparator` è un interfaccia funzionale è un'interfaccia funzionale che consente di definire un ordinamento personalizzato per una classe di oggetti.
>
>Una classe che implementa `Comparator` deve fornire un metodo `compare()` che confronta due oggetti della stessa classe e restituisce un valore intero che indica l'ordinamento tra i due oggetti, proprio come `comparable`.
>
>**Differenze:**
>- `Comparable` è un'interfaccia che deve essere implementata dalla classe stessa, mentre `Comparator` è un'interfaccia che può essere implementata da una classe esterna.
>- `Comparable` definisce un ordinamento naturale per la classe, mentre `Comparator` definisce un ordinamento personalizzato.
>  
>>[!example]- Esempio
>>
>>```java
>>public class PersonaComparator implements Comparator<Persona> { 
>>
>>@Override 
>>public int compare(Persona persona1, Persona persona2) { 
>>	if (persona1.getEta() < persona2.getEta()) {
>>		return -1;
>>	}
>>	else if (persona1.getEta() > persona2.getEta()) {
>>		return 1;
>>	}
>>	else {
>>		return persona1.getNome().compareTo(persona2.getNome()); {
>>	}
>>}
>>```

>[!warning] Interfacce Generiche
>
>`Comparable` e `Comparator` sono generiche ed il tipi in input dei metodi sono indicati con il paramentro generico `T`. E quando vengono implementate si deve specificare il tipo di oggetto che si vuole confrontare
>
>```java
>public interface Comparable<T> {     
>	int compareTo(T o); 
>}
>
>public interface Comparator<T> { 
>	int compare(T o1, T o2); 
>}
>```

## Cloneable 

Interfaccia segna posto vedi [[Java - Clone Method]] per saperne di più.

## Serializable

L'interfaccia `Serializable` in Java è un'interfaccia segna posto (cioè non contiene metodi) che indica che un oggetto può essere serializzato, ovvero convertito in un flusso di byte che può essere scritto su un file o inviato su una rete.