---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: true
created: 2025-01-28T22:37
updated: 2025-02-09T11:00
---
In Java, l'[[#Upcasting|upcasting]] e il [[#Downcasting|downcasting]] sono due concetti fondamentali nella programmazione orientata agli oggetti ([[OOP]]) che si riferiscono alla conversione di tipi di dati tra classi e sottoclassi.

### Upcasting

L'upcasting è il processo di ***conversione*** del *tipo del riferimento di un oggetto* nel tipo della sua ***super classe***. 

Ci permette trattare un oggetto come se fosse un oggetto della super classe, accedendo soltanto ai metodi e campi della super classe.

Questo può avvenire anche con un **casting implicito**.

>[!example]- Esempio
>
>```java
>public class Animale {
>    public void mangia() {
>        System.out.println("L'animale mangia");
>    }
>}
>
>public class Cane extends Animale {
>    public void abbaia() {
>        System.out.println("Il cane abbaia");
>    }
>}
>
>public class Main {
>    public static void main(String[] args) {
>        Animale animale = new Cane();
>        Cane cane = (Cane) animale; // Downcasting esplicito
>        cane.abbaia(); // Stampa "Il cane abbaia"
>    }
>```
>
>Oppure:
>
>```java
>Cane c = new Cane();  // (Cane estende Animale)
Gatto g = new Gatto();  // (Gatto estende Animale)
  >
>ArrayList<Animale> animali = new ArrayList<Animale>();  
>animali.add(c);  // casting implicito
>animali.add(g);  // casting implicito
>
>```

### Downcasting

l downcasting è il processo di ***conversione*** del *tipo del riferimento di un oggetto* nel tipo di una sua ***sottoclasse***.

Ci permette trattare un oggetto come se fosse un oggetto di una sua sotto classe, accedendo ai sui specifici metodi e campi.

Questo deve avvenire con un **cast esplicito** e se la il tipo specificato non corrisponde a quello dell'oggetto viene sollevata un eccezione.

>[!example]- Esempio Corretto
>
>```java
>public class Animale {
>    public void mangia() {
>        System.out.println("L'animale mangia");
>    }
>}
>
>public class Cane extends Animale {
>    public void abbaia() {
>        System.out.println("Il cane abbaia");
>    }
>}
>
>public class Main {
>    public static void main(String[] args) {
>        Animale animale = new Cane();
>        Cane cane = (Cane) animale; // Downcasting esplicito
>        cane.abbaia(); // Stampa "Il cane abbaia"
>    }
>}
>```

>[!example]- Esempio Errato
>
>```java
>public class Animale {
>    public void mangia() {
>        System.out.println("L'animale mangia");
>    }
>}
>
>public class Cane extends Animale {
>    public void abbaia() {
>        System.out.println("Il cane abbaia");
>    }
>}
>
>public class Gatto extends Animale {
>	public void miagola() {
>		System.out.println("Il gatto miagola");
>	}
>}
>
>public class Main {
>    public static void main(String[] args) {
>        Animale animale = new Gatto();
>        Cane cane = (Cane) animale; // Downcasting errato
>        cane.abbaia(); // Genera un'eccezione ClassCastException
>    }
>}
>
>```

### Osservazioni

>[!warning] Casting Implicito ed Esplicito
>
>- Il **casting implicito** avviene quando il ***compilatore*** può ***determinare automaticamente il tipo*** di conversione
>- Il **casting esplicito** richiede l'***uso di parentesi*** per specificare il tipo di conversione.

>[!warning] Oggetto in Memoria
>
>Il casting non cambia il tipo dell'oggetto in memoria, ma solo come viene visto dalla variabile che lo contiene.
