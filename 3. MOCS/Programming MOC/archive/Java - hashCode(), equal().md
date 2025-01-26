---
type: Programming Note
programming language: "[[Java MOC]]"
related: 
completed: false
created: 2024-09-12T17:03
updated: 2025-01-26T17:26
---
I metodi `equals()` e `hashcode()` sono metodi particolari in java che ogni oggetto eredita dalla classe `java.lang.Object`

### Equals 

Il metodo `equals()` è utilizzato per verificare se due oggetti sono uguali.

Nella sua implementazione di base presente in `Object` controlla se i due oggetti si riferiscono alla stessa area di memoria.

### Hash Code


```Java
class Recepi {
	String name;
	int difficulty ;
	String[] ingredients;
}
```


## HashCode

```java
@Override
public int hashCode() {
	int result = 17
	result *= 31 * name.hashCode();
	result *= 31 * difficulty.hashCode();
	result *= 31 * ingredients.hashCode();
	return result
}

```

---
## Equals

```java
@Overrride
public boolean equals(Object o) {
	if (this == 0) return true;
	if (o == null) return false;
	if (this.getClass() != o.getClass()) return false;

	Ricetta that = (Ricetta) o;
	return Object.equals(name, that.name) &&
		   Object.equals(difficulty, that.difficulty) &&
		   Object.equals(ingredients, that.ingredients);
}
```

- Per confrontare tipi primitivi si usa: ==
- Per confrontare degli array si usa: ?
- Per confrontare enum si usa: ?
- per confrontare oggetti si usa: equals()
