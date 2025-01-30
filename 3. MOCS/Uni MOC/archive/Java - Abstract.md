---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: true
created: 2025-01-26T14:57
updated: 2025-01-27T09:53
---
Abstract è un modificatore che può essere utilizzato soltanto su `classi` e `metodi`:

>[!note] Classi Astratte
>
>Una classe astratta, a differenza di una classe non astratta, non può essere istanziata direttamente, ma soltanto attraverso una sottoclasse che la estende.
>
>Una classe astratta, oltre a contenere dei campi, può contenere sia metodi astratti che non, mentre una classe non astratta può contenere soltanto metodi non astratti.

>[!note] Metodi Astratti
>
>Un metodo dichiarato come abstract non fornisce nessuna implementazione.
>
>Una sotto classe non astratta deve fornire un implementazione di tutti i metodi astratti della sua superasse. Con l'unica condizione che deve rispettare la segnatura del metodo ovvero il nome del metodo, il tipo di ritorno, i parametri in input e il [[Java - Access Modifier|modificatore di accessibilità]].

