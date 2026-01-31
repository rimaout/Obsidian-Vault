---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: true
created: 2025-02-08T12:15
updated: 2026-01-31T13:32
---
## Strutture dati comuni

Le liste che estendono `AbstarctList` ovvero:
- [[Java - Lists#ArrayList|ArrayList]]
- [[Java - Lists#LInkedList|LinkedList]] (implementa [[Java - Queue & Stack#Queue|Queue]])

Gli insiemi che estendono `AbstractSet` ovvero:
- [[Java - Sets#HashSet|HashSet]]
- [[Java - Sets#TreeSet|TreeSet]] 
- [[Java - Sets#LinkedHashSet|LinkedHashSet]] (estende [[Java - Sets#HashSet|HashSet]])

Le mappe che estendono `Abstact Map` ovvero:
- [[Java - Maps#HashMap|HashMap]]
- [[Java - Maps#TreeMap|TreeMap]]
- [[Java - Maps#LinkedHashMap|LinkedHashMap]] (estende [[Java - Maps#TreeMap|HashSet]])

## Come scegliere la giusta struttura dati

Come si vuole accedere alla agli elemento?
- ***Posizione*** usa `Array` o `Liste`
- ***Chiave*** usa `Mappe`
- ***Non importa*** usa `Insiemi`

È importante avere un ordinamento?
- ***Ordine Naturale*** usa [[Java - Maps#TreeMap|TreeMap]] o [[Java - Sets#TreeSet|TreeSet]] 
- ***Ordine di Inserimento*** usa [[Java - Lists#ArrayList|ArrayList]], [[Java - Lists#LInkedList|LinkedList]], [[Java - Sets#LinkedHashSet|LinkedHashSet]] o [[Java - Maps#LinkedHashMap|LinkedHashMap]]
- ***Ordine non importante*** usa [[Java - Sets#HashSet|HashSet]] o [[Java - Maps#HashMap|HashMap]]

Quali operazioni devono essere "veloci"?
- ***Ricerca*** usa [[Java - Sets#HashSet|HashSet]] o [[Java - Maps#HashMap|HashMap]]
- ***Aggiunta / Rimozione*** di elementi usa [[Java - Lists#LInkedList|LinkedList]]
- ***Non importa*** [[Java - Lists#ArrayList|ArrayList]]

