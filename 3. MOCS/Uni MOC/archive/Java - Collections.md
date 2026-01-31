---
type: Uni Note
class: Java
academic year: 2024/2025
related:
  - "[[Metodologie di Programmazione (class)]]"
completed: true
created: 2025-02-07T11:24
updated: 2026-01-31T13:32
---
## Introduzione

Le strutture servono a memorizzare e organizzare i dati in memoria in modo da poterli utilizzare efficientemente. In Java le principale strutture dati sono implementate attraverso una serie di interfacce che formano il Java Collection Framework.

Le collection si possono dividere in 3 categorie:
- [[Java - Lists]]
- [[Java - Sets]]
- [[Java - Maps]]

Le collection si bassano su una gerarchia di interfacce dove l'interfaccia `collection<E>` ne è la radice.

>[!note] Gerarchia delle Collection
>
>`Colllection` è l’interfaccia madre di tutte le collezioni in Java e questa estende l'interfaccia `Iterable` per permettere di iterare su gli elementi di una collezione.
>
>Poi ci sono tre principali **interfacce**:
>- `Set`: collezioni non ordinate che non possono contenere duplicati.
>- `List`: collezioni ordinate che possono contenere duplicati
>- `Queue`: collezioni basate sulla struttura FIFO (first in first out)
>
>![[Pasted image 20250207121850.png|700]]

>[!note] Mappe
>
>Le mappe sono strutture dati che associano ad ogni valore una chiave, e sono implementate attraverso l'interfaccia `Map`, che nonostante faccia parte del *Java Collection Framework* non estende l'interfaccia `Collection`.
