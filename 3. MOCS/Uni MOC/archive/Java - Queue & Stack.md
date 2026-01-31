---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: true
created: 2025-02-08T11:44
updated: 2026-01-31T13:32
---
## Queue

La coda è una struttura di tipo **FIFO** quindi *First In First Out*, possiamo utilizzarla implementando l’interfaccia `Queue<E>`, ad esempio è implementata dalla [[Java - Lists#LInkedList|LinkedList]].

Ci sono metodi più comuni come `add(T obb)` e `remove()` (elimina il primo elemento) e più specifici come `peek()` che ritorna il primo elemento della coda senza eliminarlo.

## Pila

La pila è una struttura dati di tipo **LIFO** quindi *Last In First Out*, per mette l’implementazione della ricorsione contendendo i record di attivazione alla chiamate dei metodi.

La classe `Stack` (ovvero una pila) implementa l'interfaccia `List` e i metodi che contiene sono:
- `push(Object Obb)` che inserisce un oggetto in cima alla pila.
- `pop()` che che rimuove l'elemento in cima alla pila.
- `peek()` che restituisce l'oggetto in cima alla pila ma senza rimuoverlo.