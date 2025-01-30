---
type: Programming Note
programming language: "[[Java MOC]]"
related: 
completed: false
created: 2024-09-12T17:03
updated: 2025-01-28T17:32
---
I metodi `equals()` e `hashcode()` sono metodi importanti in java che ogni oggetto eredita dalla classe `java.lang.Object`

- [[#Equals]]
- [[#HashCode]]

---
## Equals 

Il metodo `equals()` è un metodo importante in Java che viene utilizzato per verificare se due oggetti sono uguali. 

>[!note] Implementation Inside Object 
>Nella sua implementazione di base presente in `Object`, il metodo `equals()` controlla se i due oggetti si riferiscono alla stessa area di memoria, ovvero se sono lo stesso oggetto.

##### Override

Molte volte due oggetti anche se non uguali (ovvero non condividono la stessa area di memoria) possono essere considerati **logicamente uguali**, *ovvero hanno gli stessi attributi o proprietà*.

Ad ***esempio***,  se abbiamo due oggetti di tipo `Persona` con gli stessi attributi `nome` e `cognome`, ma che si riferiscono a due aree di memoria diverse, il metodo `equals()` di base restituirà `false`, anche se i due oggetti sono logicamente uguali.

>[!danger] Equals Override
>
>>🔥 **Importante:** Se equals viene sovrastato allora dobbiamo ri-implementare anche `hashCode()`.
>
>Per sovrascrivere `equals()` in modo tale che controlli se due oggetti sono logicamente uguali dobbiamo:
>
>1. **Verificare se l'oggetto è null**: il primo passo è verificare se l'oggetto passato come parametro è null. Se è null, il metodo `equals()` deve restituire false.
>2. **Verificare se l'oggetto è dello stesso tipo**: il secondo passo è verificare se l'oggetto passato come parametro è dello stesso tipo della classe in cui si sta sovrascrivendo il metodo `equals()`. Se non è dello stesso tipo, il metodo `equals()` deve restituire false.
>3. **Confrontare le proprietà**: il terzo passo è confrontare le proprietà dell'oggetto passato come parametro con le proprietà dell'oggetto corrente. Se le proprietà sono uguali, il metodo `equals()` deve restituire true.
>4. **Restituire il risultato**: il quarto passo è restituire il risultato del confronto.
>
>Ecco un esempio di come sovrascrivere il metodo `equals()` in una classe `ricetta`:
>```java
>class Recipe {
>	String name;
>	int difficulty ;
>	String[] ingredients;
>	
>	@Override
>	public boolean equals(Object obj) {
>		if (obj == null) return false;
>		
>		if (this == obj) return true;
>		
>		if (!(obj instanceof Recepi)) return false;
>		
>		Recepi other = (Recepi) obj;
>		return this.name.equals(other.name) && 
>			   this.difficulty == other.difficulty && 
>			   Arrays.equals(this.ingredients, other.ingredients);
>		}
>}
>```

>[!warning] Come confrontare due "variabili"
>
>- Per confrontare tipi ***primitivi*** si usa: *\=\=*
>- Per confrontare ***enum*** si usa: *\=\=*
>- Per confrontare degli ***array*** si usa: `Arrays.equals()`
>- Per confrontare ***oggetti*** si usa: `equals()`

---
## HashCode

`hashCode()` è un metodo di `object` che associa ad ogni oggetto un *codice hash* (ovvero un numero intero) che sarà lo stesso per due oggetti uguali.

Il metodo `hashcode` è utilizzato nelle strutture dati `HashMap` e `HashSet`, che utilizzando il codice di hash per organizzare gli oggetti.

>***Osservazione:*** Se due oggetti sono uguali secondo `equas()` allora dovranno avere lo stesso *hash code*, tuttavia se due oggetti hanno lo stesso *hash code* non implica che siano necessariamente uguali secondo il metodo `equals()`

>[!note] Implementation Inside Object 
Nella sua implementazione di base presente in `Object`, il metodo `hashCode()` restituisce un valore intero che rappresenta l'indirizzo di memoria dell'oggetto.

##### Override

l'implementazione di basi può non essere sufficiente, infatti molte volte due oggetti anche se non uguali (ovvero non condividono la stessa area di memoria) sono logicamente uguali ovvero hanno gli stessi attributi o proprietà.

>[!danger] HashCode Override
>
>>🔥 **Importante:** Se `equals()` viene sovrascritto allora dobbiamo ri-implementare anche `hashCode()`.
>
>Per sovrascrivere `hashCode()` in modo tale che generi lo stesso codice hash per due oggetti logicamente uguali dobbiamo:
>
>**1. Numeri Primi:** 
>- Scegliamo 2 numeri primi, uno è utilizzato per inizializzare il codice hash, l'altro per moltiplicare i valori dei campi dell’oggetto.
>- Utilizziamo dei numeri primi perché migliorano la distribuzione, ovvero ci assicurano che sia meno probabile che due oggetti diversi abbiano lo stesso *hash code*.
>
>**2. Hash dei Campi:** 
>- Si deve calcolare il *codice hash* di ogni campo dell'oggetto
>- Per data type primitivi si utilizza direttamente il loro valore come *hash code*, per gli altri campi si utilizza il metodo `hashCode()`
>
>**3. Somme e Prodotto:** 
>1. si inizializza il valore del' `hash` con il primo numero primo che si è scelto.
>2. per ogni campo del oggetto:
>	- si moltiplica il valore dell `hash` con il secondo numero primo.
>	- poi sommiamo al nuovo `hash` l'hash code del campo che si sta prendendo in considerazione
>
>Ecco un esempio di come sovrascrivere il metodo `hashCode()` in una classe `ricetta`:
>```java
>class Recipe {
>	String name;
>	int difficulty ;
>	String[] ingredients;
>	
>	@Override
>	public int hashCode() {
>		int result = 17;
>		result = 31 * result + name.hashCode();
>		result = 31 * result + difficulty;
>		result = 31 * result + Arrays.hashCode(ingredients);
>		return result;
>	}
>}
>```

