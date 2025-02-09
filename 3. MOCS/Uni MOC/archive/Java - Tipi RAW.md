---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: true
created: 2025-02-06T19:25
updated: 2025-02-06T22:34
---
I tipi generici sono stati implementati nella versione di Java 5, e per mantenere la retro compatibilità con il vecchio codice è possibile istanziare delle classi generiche senza definire alcun tipo.

```java
ArrayList<Integer> p1 = new ArrayList<Integer>(10);
ArrayList p2 = new ArrayList(10);
```
