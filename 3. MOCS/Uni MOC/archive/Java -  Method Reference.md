---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: true
created: 2025-02-10T15:17
updated: 2025-02-11T10:08
---
In Java il simbolo `::` è chiamato **operatore di riferimento a metodo**, permette di fare riferimento a metodi senza invocarli direttamente attraverso una lambda expression.

Esistono 4 principali tipi di riferimenti a metodo:
- Riferimento a un metodo statico: `Class::staticMethod`
- Riferimento a un metodo di istanza su un oggetto specifico: `object::Method`
- Riferimento a metodo di istanza su un oggetto arbitrario: `Class::Method`
- Riferimento a un costruttore: `Class::new`

Può essere utilizzato per passare un riferimento a un metodo come argomento a un altro metodo o implementare un interfacce funzionale.