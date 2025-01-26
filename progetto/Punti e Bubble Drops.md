---
type: Uni Note
class: 
academic year: 2023/2024
related:
  - "[Relazione Bubble Bobble](Relazione%20Bubble%20Bobble)"
completed: false
created: 2024-08-28T13:23
updated: 2025-01-20T20:01
---
Senza l'utilizzo di abilità speciali, l'unico modo per eliminare i nemici è catturarli in una bolla e poi farla esplodere. Ogni volta che il giocatore fa esplodere una bolla contenente un nemico, si verificano due eventi:

1. Il giocatore guadagna punti.
2. Viene generato un frutto.

La quantità di punti e il tipo di frutto generato dipendono dalla quantità di bolle contenenti nemici che vengono fatte esplodere consecutivamente. Questo meccanismo viene gestito attraverso l'esplosione a catena.

### Esplosioni a Catena

Questa è una delle meccaniche più interessanti. Infatti, ogni volta che una bolla esplode, provoca automaticamente l'esplosione di tutte le bolle con cui è in contatto. Maggiore è il numero di `EnemyBubbles` fatte esplodere consecutivamente, più alta sarà la ricompensa.

| Bolle Nemiche eliminate consecutivamente | 1                                | 2                                 | 3                                | 4                                    | 5                                 | 6                                   | 7                                 |
| ---------------------------------------- | -------------------------------- | --------------------------------- | -------------------------------- | ------------------------------------ | --------------------------------- | ----------------------------------- | --------------------------------- |
| Valore Esplosione                        | 1000                             | 2000                              | 4000                             | 8000                                 | 16,000                            | 32,000                              | 64,000                            |
| Alimento                                 | ![75](bubble_bobble_apple.png%5C) | ![75](bubble_bobble_pepper.png%5C) | ![75](bubble_bobble_grape.png%5C) | ![75](bubble_bobble_Persimmon.png%5C) | ![75](bubble_bobble_cherry.png%5C) | ![75](bubble_bobble_mushroom.png%5C) | ![75](bubble_bobble_banana.png%5C) |
| Valore Alimento                          | 1000                             | 2000                              | 3000                             | 4000                                 | 5000                              | 6000                                | 7000                              |

![bubblechainreactionexample](bubblechainreactionexample.png)