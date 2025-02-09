---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: true
created: 2025-01-29T19:14
updated: 2025-02-07T10:01
---
In Java, l'overloading e l'overriding sono due concetti fondamentali della programmazione orientata agli oggetti ([[OOP]]).

### Overloading

L'overloading si riferisce alla possibilità di definire più metodi con lo stesso nome all'interno di una stessa classe, ma con numero e/o tipo di parametri diversi. 

Ciò significa che il metodo può essere chiamato con argomenti diversi, e il compilatore Java sceglierà il metodo corretto in base ai parametri passati.

>[!note] Regole per l'Overloading
>
>- ***Stesso nome:*** i metodi devono avere lo stesso nome.
>- ***Parametri diversi:*** i metodi devono avere parametri diversi (numero, tipo o ordine).
>- ***Tipo di ritorno:*** il tipo di ritorno dei metodi può essere diverso, ma non è necessario.
>- ***Modificatore di accesso:*** il modificatore di accesso può essere diverso, ma non è necessario.

>[!example]- Esempio
>
>```java
>public class Test {  
>      
>    private String Esperimento(int i) {  
>        return "Ciao" + i;  
>    }  
>  
>    private String Esperimento() {  
>        return "Mamma";  
>    }  
>  
>    public int Esperimento(int i, int j) {  
>        return i + j;  
>    }  
>}
>```

>**Extra:** [[Java - Generic Types#Overloading Metodi Generici|Overloading di un metodo Generico]]

### Overriding

L'overriding si riferisce alla possibilità di ri-implementare un metodo di una classe padre all'interno di una classe figlia. 

>[!note] Regole per l'Overriding
>
>- ***Stessa intestazione:*** il metodo deve avere la stessa intestazione (stesso tipo di output, stessi campi in input).
>- ***Modificatore di accesso:*** il modificatore di accesso può essere diverso, ma deve essere uguale o più forte (ad esempio, si può usare `public` se il metodo padre era `protected`, ma non si può usare `private` se il metodo padre era `public`).
>- ***Metodi final o private:*** non si può fare un override di un metodo `final` o `private`.
>  
>  Inoltre, è importante utilizzare l'annotazione `@Override` per indicare al compilatore che si sta ridefinendo un metodo esistente.

>[!example]- Esempio
>
>```Java
>public class Animale {
>    public String suona() {
>        return "L'animale fa un rumore";
>    }
>}
>
>public class Cane extends Animale {
>    @Override
>    public String suona() {
>        return "Il cane abbaia";
>    }
>}
>
>public class Gatto extends Animale {
>    @Override
>    public String suona() {
>        return "Il gatto miagola";
>    }
>}
>```