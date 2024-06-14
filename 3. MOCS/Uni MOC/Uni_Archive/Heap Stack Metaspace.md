---
type: Uni Note
class: 
academic year: 2023/2024
related: 
completed: false
created: 2024-06-13T18:38
updated: 2024-06-13T19:03
---
---

>[!abstract] Index
>1. 

>[!abstract] Related
>- 

---

**Heap:**
Rappresenta l'allocazione degli oggetti.

**Stack:**
Rappresenta i "Frame di attivazione" ovvero:
- Chiamate ai metodi
- Variabili locali

**Metaspace:**
Rappresenta l'allocazione dei capi statici:
- quindi variabili statiche
- (forse anche metodi ????)

1. cosa analizzare capi statici
2. analizzare main (partendo da args)




>[!warning] A cosa inizializzo una capo "vuoto"
>`0` --> Variabili Numeriche (int, double, etc.)
>`null` --> Variabili Oggetto (array, stringe, etc.)
>`false` --> Variabili booleane
>
>>**Esempio:** `staic private int passaggi;` viene inizializzato a 0 nel metaspace

>[!warning] Inizializzazione di variabile (non campi)
>
>Verrano inizializzate ad `undef` se non gli diamo un valore
>
>```java
>int g = 3;        // g = 3
>int h;            // g = undef
>```
>
>>**Esempio:** `staic private int passaggi;` viene inizializzato a 0 nel metaspace

>[!warning] Args
>Inizializziamo args nella stack ma punta ad un oggetto nella heap, e quest oggetto è una array di stringe.
>
>>**oss:** l'oggetto puntao da args contiene puntatori a stinge

>[!warning] Costruttori
>se incontriamo un costruttore dobbiamo inserirlo nello stack,  e dopo va cancellato e al suo posto ci sarà l'ogetto nel main (o nel metodo che ha chiamato il costruttore)

