---
type: Programming Note
programming language: "[[Java MOC]]"
related: 
completed: false
created: 2024-09-12T17:03
updated: 2024-09-12T17:57
---
>[!abstract] Index
>1. 

>[!abstract] Related
>- 

>[!danger] TLDR
>

---


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


## Compare

in questo confronterò la difficoltà

```java
@Override
public int compareTo(Recepi o) {
	if (this.difficulty > o.difficulty)
		return 1
	
	if (this.difficulty < o.difficulty)
		return -1
	
	else return 0
}
```
