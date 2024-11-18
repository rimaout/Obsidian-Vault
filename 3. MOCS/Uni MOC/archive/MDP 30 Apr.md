---
created: 2024-04-30
type: Uni Note
class: 
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
## Tipi Generici

**Creare istanze di classi con generici:**
```java
new arrayList<String>();
```

**Dichiarare e assegnare variabili di tipi generici:**
```java
List<String> listaDiStringhe = new arrayList<String>();
```

**Dichiarare metodi che prendono in input tipi generici:**
```java
public void metodo(List<String> lista){
	// code
}
```

**Esempio Classe Generica:**
```java
public class valore<T>{
	private final T val;
	
	public Valore(T va ) {this.val = val;}

	public T get() {return val;}

	public String toSTring() {return "" + val;}

	public String getType() {return val.getClass().getName();}
}
```

- Per definire un tipo generico della classe, si utilizza la sintassi a parentesi angolari dopo il nome della classe con il tipo generico da utilizzare
- Da quel punto, si utilizza il tipo generico come un qualsiasi altro tipo di classe

**Istanziare la classe generica:**


**Specificare più tipi generici di classe:**


**I generici funzionano solo con i tipi derivati:**


**I tipi generici differiscono sulla base dei loro tipi:**


**Estendere le classi generiche:**

- Ovviamente è possibile estendere le classi generiche per creare classi più specifiche
- Esempio orario estende classe coppia::

---
**Esercizio: Lista Linkata generica:**
```java
public class ListaLinkata<T>{
	private Elemento first;

	private class Elemento{
		private T val;
		private Elemento next;
		public Elemento(T val, Elemento next) {this.val = val}
	}

	public void addFirst(T e){
		first = new Elemento(e, first);
	}

	public void removeFirst(){
		first = first.next;
	}

	public String toString(){
		StringBuffer sb = new String Buffer()	;
		Elemento e = first;

		while(e != null) {
			sb.append(e.val); 
			if (e.next != null) sb.append(",");
			e = e.next;	
		}
		return sb.toString();
	}
}
```

**Le interfacce Comparable e Comparator sono generiche:**


**Estendere Interfaccia con vincolo di comparabilità:**
```java
public interface MinMax<T extends Comparable<T>>{
	T min();
	T max();
}
```
- Stiamo dicendo che il tipo deve essere un tipo comparabile se vuole implementare MinMax

Esempio teorico:
```java
public class MyClass <T  extends Comparable<T>> implemets MinMax<T>{
	//code
}
```

Esempio reale:
```java
public class MyClass implements MinMax<Integer>{
	//code
}
```

**Definire metodo generico senza ritorno:**
```java
static public <T> void esamina(ArrayList<T> lista){
	for (T 0 : lista)
		System.out.println(o.toString());
}
```

**Definire metodo generico ritorno generico:**

```java
static public <T> T esamina(ArrayList<T> lista){
	for (T o : lista)
		return o;
		
} 
```

**Definire metodo generico con tipo definito:**

```java
static public <T> String esamina(ArrayList<T> lista){
	for (T o : lista)
		return o.toString();
		
} 
```

>[!warning] 
>- Ogni volta che un metodo ha come input un tipo generico deve avere `<T>` prima del tipo del metodo
>- Il controllo di consistenza di tipo viene effettuato a tempo di compilazione

**Jolly ?:**

```java
Public static void mangia(Array<? extends Mangiabile> frutta){
	//code
}
```

il jolly si può utilizzare sen non mi serve il simbolo nella classe

```java
public static <T extends Mnagiabile> void magia(ArrayList<T> frutta){
	//java
}
```
- Sono equivalenti (in questo caso) ma il secondo non ha nozione del tipo utilizzato

**Usare \<?> per prendere in input un oggetto di una
classe con qualsiasi tipo parametrico:**

- Nel caso in cui non sia necessario conoscere il tipo parametrico, si può utilizzare \<?>

Esempio:
```java
public class Punto<T extends Number>{
	private T x;
	private T y;

	public Punto(T x, T y) {
		this.x = x;
		this.y = y;
	}

	sdbhx lhghkjhvk jbzjkl l 
}
```

**Type Ensure:**



Pecs

Sta per, quando devi fare operazioni di produzione che consumano gli elementi  effettui operazioni con questo protocollo qua ...

continua in [[MDP 02 May]]

