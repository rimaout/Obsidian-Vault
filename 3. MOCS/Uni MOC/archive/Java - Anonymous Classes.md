---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: true
created: 2025-02-02T20:45
updated: 2025-02-09T18:42
---
Le classi anonime in Java sono classi che non hanno un nome esplicito. Sono utilizzate per creare oggetti che implementano un'interfaccia o estendono una classe, senza dover definire una classe separata.

Utili quando si deve fornire un implementazione personalizzata di una classe o di un interfaccia e tale implementazione deve essere utilizzata una singola volta nel codice.

```java
interface Formula {
	double calcola(int a);
	default double sqrt(int a) {return Math.sqrt(a); }
}
```

```java
public class Esempio {
	public static void main(String[] args) {
    // Creazione di una classe anonima che implementa l'interfaccia Formula

    Formula formula = new Formula() {
		public double calcola(int a) {
			return sqrt(a * 100);
		}
	};
  }
}
```

>[!note] Memoria 
>
>Sono compilate come le classi interne, quindi vanno nella *heap* ma non hanno un tipo definito e il `this` si riferisce all'oggetto anonimo della classe estesa.
>
>***Differenza con*** [[Java - Lambda Expressions]]

