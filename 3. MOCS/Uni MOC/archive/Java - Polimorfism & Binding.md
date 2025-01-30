---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: true
created: 2025-01-29T16:25
updated: 2025-01-30T16:15
---
## Polimorfismo

Il polimorfismo è un concetto fondamentale della programmazione orientata agli oggetti ([[OOP]]). 

In generale, si riferisce alla capacità di un oggetto di assumere diverse forme o comportamenti a seconda del contesto in cui viene utilizzato.

Più nello specifico permette di utilizzare lo stesso codice su oggetti diversi, ma che condividono una classe madre. Ciò significa che possiamo creare codice che funziona con oggetti di tipo diverso (ma che ereditano le stessa classe), senza dover scrivere codice specifico per ogni tipo di oggetto.

>[!example] Esempio
>
>Possiamo creare una lista di `Forme` che contiene allo stesso momento oggetti di tipo `Triangolo`, `Quadrato` e `Rettangolo`, perché tutti questi oggetti estendono la classe `Forma`. Inoltre, per ogni forma nella lista potremmo chiamare il metodo `calcolaArea()` e verrà utilizzato il metodo specifico per ogni tipo di forma.

## Binding

Il binding è il processo che determina quale oggetto deve essere utilizzato quando si chiama un metodo o si accede a una variabile.

Infatti per la presenza di polimorfismo, il tipo del riferimento (variabile) può non corrispondere al tipo dell'oggetto vero e proprio presente in memoria.

>[!note] Binding Statico
>
>*Binding Statico* (o early binding) si verifica quando il tipo di un oggetto o di un metodo viene determinato **durante la compilazione** del codice.
>
>Si utilizza per tutti quei *metodi* che ***non possono essere sovrascritti*** dalle sotto classi ovvero metodi:
>- `statici`
>- `private`
>- `final`

>[!note] Binding Dinamico
>
*Binding Dinamico* (o late binding) si verifica quando il tipo di un oggetto o di un metodo viene determinato **durante l'esecuzione** del codice.
>
>Il metodo effettivo viene determinato a run time in base al tipo concreto dell'oggetto e non al tipo della variabile di riferimento.
>
>Ad esempio:
>
>```java
>Animal animale = new Cane(); animale.abbaia();
>```
>
>In questo caso, il compilatore non può determinare con certezza quale metodo `abbaia()` verrà chiamato, perché il tipo della variabile `animale` è `Animal`, ma l'oggetto vero e proprio è di tipo `Cane`. A runtime, il sistema verifica il tipo dell'oggetto e chiama il metodo `


