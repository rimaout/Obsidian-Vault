---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: true
created: 2025-02-02T22:33
updated: 2025-02-09T16:51
---
## Introduzione[[
]]
I tipi generici in Java sono un potente meccanismo che permette di scrivere codice flessibile e riutilizzabile; dando la possibilità di definire classi, interfacce e metodi che operano su tipi di dati specificati solo al momento dell'utilizzo.

Ad esempio le [[Java - Collections|collezioni]] sono classi generiche dove il tipo su cui operano è definito soltanto al momento dell'istanziazione attraverso l'*operatore diamante* `<>`. Questo ha permesso di utilizzare un singolo codice per creare delle collection per qualsiasi tipo, ad esempio senza i tipi generici si sarebbe dovuto difinire un tipo specifico di ArrayList per ogni tipo d'oggetto esistente.

```java
ArrayList<Sting> lista = ArrayList<>();
```

>[!danger] Implementazione dei Tipi Generici
>
>I tipi generici sono implementati attraverso la cancellazione del tipo. Vedi [[Java - Cancellazione del Tipo  (type erasure)]] per saperne di più

## Limiti

>[!note] No Primitivi
>
>Non è possibile utilizzare i tipi primitivi con tipi generici, questo perché durante la [[Java - Cancellazione del Tipo  (type erasure)|cancellazione del tipo]], il tipo generico viene sostituito con Object e i primitivi non possono essere trattati come oggetti.

>[!note] No ereditarietà dei tipi generici
>
>Per le classi generiche non vale l'ereditarietà dei tipi generici ovvero `ArrayList<Integer>` non è di tipo `ArrayList<Number>` o `ArrayList<Object>`, quindi non possiamo fare:
>
>```java
>ArrayList`<Number> listaNumeri = new ArrayList<Integer>(); //errore
>```
>
>Ma rimane comunque l'ereditarietà tra classi:
>
>```java
>List`<Integer> listaNumeri = new ArrayList<Integer>();
>```

>[!note] No upcasting 
>
>Non è permesso l'upcasting nei tipi generici, ad esempio:
>
>Creiamo una lista di mele
>
>```java
>`ArrayList<Mela> mele = new ArrayList<Mela>();
>```
>
>Definiamo un metodo che prende in input una lista di frutti e inserisce una pera (sotto classe di frutto)
>
>```java
>public static void aggiungiPera(`ArrayList<Frutto> frutti) {
>    frutti.add(new Pera());
>}
>```
>
>Ora, proviamo a utilizzare la lista di mele come input del metodo appena citato.
>
>```java
>aggiungiPera(mele);
>```
>
>Tuttavia, questo ci darà un errore di compilazione. Il motivo è che il metodo `aggiungiPera` prende in input una lista di frutti, mentre noi gli stiamo passando una lista di mele. Questo non è possibile perché non si può fare l'upcasting dei tipi generici.
>
>Se fosse possibile, avremmo come risultato una lista di mele che contiene una pera, il che non è corretto. La lista di mele dovrebbe contenere solo mele, non frutti di tipo diverso.
>
>>*oss:* Le collection (come `ArrayList`) sono generiche.
>
>Tuttavia, possiamo l’[[Java - Jolly Operator (?)|operatore jolly]] `?`  con `? extends Frutto` per definire un metodo che può prendere in input una lista di frutti o di qualsiasi sua sottoclasse.
>
>In questo caso, il metodo non può aggiungere un elemento alla lista, ma può leggere gli elementi presenti nella lista.

## Da sapere

>[!note] Estendere Classi Generiche
>
>È possibile estendere classi generiche o implementare interfacce generiche con classi a loro volta generiche, è possibile scegliere il tipo nelle loro sotto classi.
>
>```java
>public class ClasseBase`<T>` { 
>	private T valore; 
>	
>	public ClasseBase(T valore) { 
>		this.valore = valore; 
>	} 
>} 
>
>public class ClasseEstesa`<K, T>` extends ClasseBase`<T>` { 
>	private K chiave; 
>	
>	public ClasseEstesa(K chiave, T valore) { 
>		super(valore); 
>		this.chiave = chiave; 
>	}
>}
>```

>[!note] Vincoli sui parametri di tipo generico
>
>Puoi aggiungere vincoli sui parametri di tipo generico per specificare quali tipi di dati sono ammessi estendendo il tipo generico.
>
>```java
>`public class Collezione<T extends Numero> {   // codice della classe }`
>```
>
>In questo esempio, il parametro di tipo generico `T` è vincolato a estendere la classe `Numero`. Ciò significa che la classe `Collezione` può lavorare solo con oggetti che estendono la classe `Numer`
>

>[!note] Utilizzo di più parametri di tipo generico
>
>Puoi utilizzare più parametri di tipo generico per creare classi più complesse. Ciò ti consente di definire più di un tipo di dati che la classe può gestire.
>
>```java
>`public class Mappa<K, V> {   // codice della classe }`
>```
>
>In questo esempio, la classe `Mappa` ha due parametri di tipo generico `K` e `V`. La classe può lavorare con qualsiasi tipo di chiave (`K`) e valore (`V`). Ad esempio, potresti utilizzare la classe `Mappa` per creare una mappa di stringhe e interi, o una mappa di oggetti personalizzati e valori di tipo `Boolean`.

>[!note] Metodi generici in classi non generiche
>
>È possibile definire metodi generici in classi non generiche.
>
>Esempio:
>
>```java
>public class Esempio { 
>	public `<T>` void stampa(T elemento) { 
>		System.out.println(elemento); 
>	} 
>}
>```

---
## Overloading Metodi Generici

Un metodo generico può essere sovraccaricato anche da un metodo non generico ma con lo stesso nome e numero di parametri. Quando il compilatore riceve una chiamata a questo metodo cerca prima l'implementazione più specifica, ovvero quella non generica e poi il generico, per garantire un'ottimizzazione in base al tipo.

```java
static public<T extends Comparable<T>> T getMassimo(T a, T b, T c){ ... }
static public String getMassimo(String a, String b, String c){ ... }
```