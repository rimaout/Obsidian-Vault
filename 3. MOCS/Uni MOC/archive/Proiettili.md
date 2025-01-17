---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-01-16T16:41
updated: 2025-01-17T17:55
---

I proiettili sono una tipologia di oggetti ognuna con le sue abilità, ma che sono tutti accomunati dal fatto che si muovono orizzontalmente sulla mappa e che permettono di eliminare delle entità specifiche. 

Di tutti i "proiettili" presenti nel gioco originale io ho deciso di implementare:

| Immagine                          | Nome                         |
| --------------------------------- | ---------------------------- |
| ![[lightinigprojectile.png\|80]]  | **Lightning Projectile**     |
| ![[maitafilreprojectile.png\|80]] | **Maita Fireball Projetile** |
| ![[bollaproj.png\|80]]            | **Player Bubble Projetile**  |


##### Lightning Projectile

Il **lightning projectile** è un proiettile generato quando il player fa esplodere una **lighting bubble**. Una volta generato si muoverà orizzontalmente nella stessa direzione che il player aveva quando ha colpito la bolla.

Il proiettile si disattiva quando si interseca con il limite più esterno della mappa o quando colpisce un nemico. Quando il proiettile colpisce un nemico quest’ultimo viene eliminato.

##### Maita Fire Projectile

Il **Maita fire projectile** è un proiettile generato dal mostro `Maita`. Maita quando ha per tre secondi consecutivi line of sight con il player lancia una palla di fuoco nella direzione del player. Questo proiettile è disattivato quando colpisce un player ho quando è a contatto con un muro. Se il player è colpito perde una vita.

##### Player Bubble Projectile

Il **player bubble projectile** non è altro che l'attacco del player. Il giocatore premendo il tasto invio effettua un attacco che genera una bolla che inizialmente è in uno stato di "proiettile" in cui si muove orizzontalmente e se colpisce un nemico lo cattura.

Una volta finita la sua animazione, il proiettile si trasforma in una bolla vera e propria che può essere fatta esplodere dal player.

![[bolleprojectile.png|500]]
