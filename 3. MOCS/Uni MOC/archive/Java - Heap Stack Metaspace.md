---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2023/2024
related:
  - "[[Java MOC]]"
completed: true
created: 2024-06-13T18:38
updated: 2026-01-31T13:32
---
In Java la memoria è suddivisa in 3 aree principali `Heap`, `Stack` e `Metaspace`, dove:
- **Stack:** è la memoria più veloce ma piccola, è utilizzata per le variabili locali ed i frame di attivazione dei metodi, è una stack ovvero una pila, questo vuol dire che l'ultimo metodo chiamato sarà il primo ad essere chiuso.
- **Heap:** è la memoria più grande, ed è utilizzata per allocare istanze oggetti, quest’ultime sono puntate dalle variabili presenti nello stack.
- **Metaspace:** è utilizzato per memorizzare i metadati delle informazioni delle classi a runtime, inoltre è dove vengono allocati i capi statici (che sono i primi capi ad essere allocati di una classe).

>***Garbage Collector:*** Quando un oggetto nella heap non è più puntato da alcuna variabile, questo viene eliminato dal *garbage collector* in un momento casuale.

---

>[!warning] A cosa inizializzo una capo "vuoto"
>`0` --> Variabili Numeriche (int, double, etc.)
>`null` --> Variabili Oggetto (array, stringe, etc.)
>`false` --> Variabili booleane
>
>>**Esempio:** `staic private int passaggi;` viene inizializzato a 0 nel metaspace
>
>- I **campi non statici** vengono inizializzati solo quando chiamati da un metodo e vanno nella heap

>[!warning] Inizializzazione di variabili locali
>
>Verrano inizializzate ad `undef` se non gli diamo un valore
>
>```java
>int g = 3;        // g = 3
>int h;            // g = undef
>Object z;         // z = undef
>```
>
>>**Esempio:** `staic private int passaggi;` viene inizializzato a 0 nel metaspace

>[!warning] Args
>Inizializziamo args nella stack ma punta ad un oggetto nella heap, e quest oggetto è una array di stringe.
>
>>**oss:** l'oggetto puntao da args contiene puntatori a stinge

>[!warning] Costruttori
>se incontriamo un costruttore dobbiamo inserirlo nello stack,  e dopo va cancellato e al suo posto ci sarà l'ogetto nel main (o nel metodo che ha chiamato il costruttore)

>[!warning] Classi
>Ogni volta che incontriamo una classe (ovvero quando eseguiamo un costruttore di una classe):
>-  per prima cosa vengono allocati i campi statici (se è la prima volta che )

## Classi e Sottoclassi 

Se ci troviamo in una situazione del genere, dove:
- La classe `Persona Concreta` estende la classe `Persona` e
- sia la classe `persona` sia la classe `Persona Concreta` hanno entrambe un metodo to string

```java
Persona p1 = new PersonaConcreta(-5)
name1 = p1.toString()

PersonaConcreta p2 = new PersonaConcreta(-5)
name2 = p2.toString()
```

 In questo caso utilizziamo il metodo `toString` della classe `PersonaConcreta` e non quello di `Persona`, infatti in questi casi utilizziamo sempre i metodi della classe che è stata utilizzata per costruire l'oggetto.

Invece, se ci troviamo in una situazione del genere, dove:
- La classe `Persona Concreta` estende la classe `Persona` e
- solo la classe `persona` possiede un metodo to string

Se eseguiamo:
```java
Persona p1 = new PersonaConcreta(-5)
name1 = p1.toString()

PersonaConcreta p2 = new PersonaConcreta(-5)
name2 = p2.toString()
```

 In questo caso utilizziamo il metodo di `Persona`, sia per `p1` che per `p2`, infatti entrambi ereditano il metodo dalla classe to string