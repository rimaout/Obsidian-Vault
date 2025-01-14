---
type: Uni Note
class: 
academic year: 2023/2024
related:
  - "[[Relazione Bubble Bobble]]"
completed: false
created: 2024-08-28T13:23
updated: 2025-01-08T15:45
---

Senza l'utilizzo di abilità speciali, l'unico modo per eliminare i nemici è catturarli in una bolla e poi farla esplodere, ogni volta che il giocatore fa esplodere una bolla contenente un nemico, si verificano due eventi:
1. Il giocatore guadagna punti.
2. Viene generato un frutto.

> [!warning] Frutta 
> Il giocatore può raccogliere un frutto semplicemente passandoci sopra ricevendo dei punti, la quantità di punti ricevuti dipende dal tipo di alimento.

La quantità di punti e il tipo di drop generato dipendono dalla quantità di bolle contenenti nemici che vengono fatte esplodere consecutivamente, questo meccanismo viene gestito attraverso l'esplosione a catena.

### Esplosioni a Catena

Una delle meccaniche più interessanti è l'esplosione a catena delle bolle. Infatti, ogni volta che una bolla esplode, provoca automaticamente l'esplosione di tutte le bolle con cui è in contatto.

**Questa caratteristica è fondamentale per determinare:**
- Il numero di punti che il giocatore riceverà dall'esplosione delle bolle.
- Quale frutto verrà generato dalla bolla contenente il nemico eliminato.

Maggiore è il numero di bolle fatte esplodere consecutivamente, più alta sarà la ricompensa.

##### Punti e Alimenti in Base alle Esplosioni

| Bolle Nemiche eliminate consecutivamente | 1                                | 2                                 | 3                                | 4                                    | 5                                 | 6                                   | 7                                 |
| ---------------------------------------- | -------------------------------- | --------------------------------- | -------------------------------- | ------------------------------------ | --------------------------------- | ----------------------------------- | --------------------------------- |
| Valore Esplosione                        | 1000                             | 2000                              | 4000                             | 8000                                 | 16,000                            | 32,000                              | 64,000                            |
| Alimento                                 | ![[bubble_bobble_apple.png\|75]] | ![[bubble_bobble_pepper.png\|75]] | ![[bubble_bobble_grape.png\|75]] | ![[bubble_bobble_Persimmon.png\|75]] | ![[bubble_bobble_cherry.png\|75]] | ![[bubble_bobble_mushroom.png\|75]] | ![[bubble_bobble_banana.png\|75]] |
| Valore Alimento                          | 1000                             | 2000                              | 3000                             | 4000                                 | 5000                              | 6000                                | 7000                              |

---