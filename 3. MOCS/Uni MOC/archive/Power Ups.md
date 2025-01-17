---
type: Uni Note
class: 
academic year: 2023/2024
related:
  - "[[Relazione Bubble Bobble]]"
completed: false
created: 2024-09-02T12:47
updated: 2025-01-17T17:09
---
## Power Ups

Nel gioco originale c'è una grande quantità di diversi potenziamenti che possono essere ottenuti, completando delle "sfide", io ho deciso di implementare questi potenziamenti:

| Immagine             | Nome               | Funzione                                                                                                | Sfida                                                                   | Punti    |
| -------------------- | ------------------ | ------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- | -------- |
| ![[bb_gc.png\|80]]   | **Green Candy**    | Aumenta cadenza di fuoco delle bolle                                                                    | Sparare 35 bolle                                                        | 100      |
| ![[bb_bc.png\|80]]   | **Blue Candy**     | Aumenta velocità di movimento delle bolle                                                               | Far esplodere 35 bolle                                                  | 100      |
| ![[bb_rc.png\|80]]   | **Red Candy**      | Aumenta distanza percorsa dalle bolle                                                                   | Saltare 35 volte                                                        | 100      |
| ![[bb_s.png\|80]]    | **Shoes**          | Aumenta velocità di movimento del player                                                                | Percorrere una distanza equivalente alla lunghezza delle mappa 15 volte | 100      |
| ![[bb_rp.png\|80]]   | **Orange Parasol** | Salta 3 livelli                                                                                         | Far esplodere 15 bolle d'acqua                                          | 200      |
| ![[bb_bp 1.png\|80]] | **Blue Parasol**   | Salta 5 liveli                                                                                          | Far esplodere 20 bolle d'acqua                                          | 200      |
| ![[bb_h.png\|80]]    | **Chack'n Heart**  | Rende il player invincibile, immobilizza tutti e nemici e li rende eliminabili semplicemente toccandoli | Raccogliere 55 oggetti                                                  | 3000     |
| ![[bb_gr.png\|80]]   | **Emerald Ring**   | 500 punti per ogni salto                                                                                | Raccogliere 3  Green Candy                                              | 1000     |
| ![[bb_br.png\|80]]   | **Crystal Ring**   | 10 punti per ogni passo                                                                                 | Raccogliere 3 Blue Candy                                                | <br>1000 |
| ![[bb_rr 1.png\|80]] | **Ruby Ring**      | 100 per ogni bolla sparata                                                                              | Raccogliere 3 Red Candy                                                 | <br>1000 |

>**Funzionamento:**
>
>All'inizio di ogni livello, precisamente dopo 12 secondi, viene generato in un punto casuale della mappa un nuovo `powerup` tra quelli "disponibili". Per rendere disponibile un potenziamento si deve completare la sfida ad esso associata.
>
>Ogni volta che il player perde una vita, i powerUp ottenuti e i processi delle sfide vengono resettati.

