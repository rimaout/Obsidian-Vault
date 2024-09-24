---
type: Uni Note
class: 
academic year: 2023/2024
related:
  - "[[Relazione Bubble Bobble]]"
completed: false
created: 2024-09-16T11:41
updated: 2024-09-16T19:04
---
---

Nel gioco ci sono diversi bolle speciali, io in particolare ho deciso di implementare la bolla d'acqua è la bolla lampo.

## Water Bubble

La bolla d'acqua normalmente si comporta come le altre bolla, quindi si muove seguendo le correnti d'aria, le differenze si cominciano a notare quando viene fatta esplodere.

Infatti quando viene fatta esplodere si trasforma in un flusso d'acqua che si muove per la mamma cercando di andare verso il basso, e ogni volta che colpisce un nemico lo elimina

In più può anche catturare il player e trasportarlo in giro per la mappa, facendo ciò sarà possibile fare esplodere le altre bolle e collezionare gli item.

Il flusso d'aqua si interrompe quando raggiunge la base della mappa e cade nel vuoto (aggiungi foto), quando succede.

Quando il flusso d'acqua è interrotto, genererà i drop nella parte alta della mappa , in particolare rilascerà un cristallo d'aqua per ogni nemico catturato,  e libererà il player nella parte alta della mappa.

**Drop:**

| Immagine              | Punti |
| --------------------- | ----- |
| ![[12he3uh8.png\|75]] | 6000  |

## Lighting Bubble

La bolla lampo quando colpita crea un proiettile lampo che si muove orizzontalmente, in particolare se la bolla si trova nella metà destra della mappa il lampo andrà verso sinistra, viceversa se la bolla si trova nella parte sinistra della mappa allora il lampo andrà verso destra.

Inoltre i lampi continuano a muoversi fino a quando non colpiranno una delle pareti esterne della mappa, o un nemico