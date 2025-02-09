---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: true
created: 2025-02-07T17:38
updated: 2025-02-08T12:36
---
Gli insiemi sono [[Java - Collections|collezioni]] **prive di duplicati** che estendono la classe `AbstractSet` ed implementano l'interfaccia `Set`. Gli oggetti inseriti nei set devono implementare correttamente i metodi [[Java - HashCode & Equals Methods|hashCode() ed equals()]].

Esistono diversi tipi di set con diverse caratteristiche:
- [[#HashSet]]
- [[#TreeSet]]
- [[#LinkedHashSet]]

---
#### HashSet

Gli elementi della collezione sono memorizzai in una tabella di hash, questo implica costi di ricerca ed inserimento veloci, e l'assenza di un ordinamento degli elementi.

>[!note] Hash Table
>
>Una tabella di hash è composta da un array principale chiamato *bucket list* contenete puntatori a delle liste chiamate bucket. La funzione di hash utilizza l'hash code dell oggetto che vogliamo cercare per determinare l'indice della bucket list contenente il puntatore all bucket in cui dovrebbe essere l'oggetto che stiamo cercando. Ora basterà cercare in quel bucket per cercare l'oggetto.
>
>É quindi necessario che elementi uguali abbiano lo stesso hash code che vengano cercati nello stesso bucket e poi  confrontati con `equals()`.
>
>![[Pasted image 20250207185833.png|600]]

^3a11b6

#### TreeSet

Memorizza gli elementi della collezione in una struttura ad albero mantenendo il loro ordine naturale tramite `compareTo()`. Questa struttura ci permette di cercare, rimuovere e inserire con costo `log(n)`, dato che è possibile utilizzare la ricerca binaria.

>[!note] Alberi
>
>Gli alberi sono strutture su cui si basano molte strutture dati come: [[Java - Sets#TreeSet|TreeSet]] o [[Java - Maps#TreeMap|TreeMap]]. Sono strutture dati ricorsive, che possono essere implementate attraverso librerie come `JGraphT` e `Guava`. Il tipo di albero più semplice è un albero binario composto da nodi che hanno al massimo due figli.

^6a39b8

#### LinkedHashSet

Memorizza gli elementi in una tabella hash proprio come un [[#HashSet]] ma allo stesso tempo mantiene una copia dei dati in una struttura simile ad una [[Java - Lists#LinkedList|LinkedList]].

Questo permette di avere le prestazioni del [[#HashSet]] e allo stesso tempo mantenere l'ordinamento di inserimento attraverso la [[Java - Lists#LinkedList|LinkedList]].

Naturalmente questa struttura dati richiede più memoria ed overHead per il mantenimento della due strutture dati.