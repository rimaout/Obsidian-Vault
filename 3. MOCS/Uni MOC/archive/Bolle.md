---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-01-17T17:56
updated: 2025-01-18T17:35
---
Come si può evincere dal nome del gioco (Bubble Bobble), una delle meccaniche centrali del gameplay è la presenza di bolle, in particolare ne esistono di due categorie: `playerBubbles` e `specialBubble`.

Le caratteristiche che accomunano tutte le bolle sono:
- Il giocatore ha la capacità di **interagire** in diversi modi con le bolle, spostandole, saltandoci sopra e naturalmente facendole esplodere.
- **Esplosione a catena**: tutte le bolle vicino a una bolla esplosa esploderanno a loro volta.
- Il movimento delle bolle è influenzato dai **venti**, infatti ogni tile della mappa ha un campo di direzione del vento. Questo campo indica alle bolle che si trovano sulla tile in quale direzione muoversi.

## PlayerBubbles

Le `playerBubbles` non sono altro che le bolle generate dal giocatore stesso e ne esistono di due tipi:

| Immagine               | Nome             | Caratteristiche                                                                                                                                                                                                                                                 |
| ---------------------- | ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![[emptybubble.png]]   | **Empty Bubble** | È la bolla generata dall'attacco del giocatore ed è utilizzata per catturare i nemici.                                                                                                                                                                               |
| ![[enemybubble 1.png]] | **Enemy Bubble** | Quando una `empty bubble` colpisce un nemico, la bolla lo cattura e si trasforma in un `enemy bubble`. Le `enemy bubble` hanno un timer interno che, quando scade, libera il nemico. Se la bolla viene colpita dal giocatore e fatta esplodere, allora il nemico è eliminato. |

## SpecialBubbles

Le bolle speciali, a differenza delle `playerBubbles`, non vengono generate da un giocatore, ma spawnano automaticamente. Lo spawn delle bolle è gestito da una classe chiamata Bubble manager, che in base alle caratteristiche del livello decide dove e quali bolle creare.

Nel mio gioco sono presenti due tipi di bolle speciali:

| Immagine                | Nome                 | Caratteristiche                                                                                                           |
| ----------------------- | -------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| ![[lightingbubble.png]] | **Lightning Bubble** | Quando fatte esplodere, generano un `lighting projectile` che può essere utilizzato per eliminare i nemici. |
| ![[waterbubble.png]]    | **Water Bubble**     | Quando fatte esplodere, generano un `water flow`.                                                                           |

## Water Flow

Quando una bolla d'acqua esplode, viene generato un `waterFlow`, un oggetto d'acqua che cattura ed elimina tutti i nemici lungo il suo percorso. Può anche catturare il giocatore che per tutto il percorso del `waterFlow` perderà la capacità di muoversi liberamente.

Una volta che il `waterFlow` raggiunge la base della mappa e cade nel vuoto:
- il giocatore verrà spawnato nella parte alta della mappa;
- per ogni nemico catturato dalla flusso d'acqua, verrà generato un item a forma di cristallo d'acqua del valore di 1000 punti.

![[Screenshot 2025-01-17 at 22.51.27.png|700]]
## Informazioni aggiuntive

Come detto in precedenza, le bolle si muovono nella mappa seguendo i venti. Ad ogni tile è associata una direzione e le bolle possono controllare in che direzione muoversi semplicemente accedendo a questo campo della tile. Ciò permette di creare livelli con correnti d'aria che spostano le bolle per la mappa, con la possibilità di creare dei punti di accumulazione.
![[Screenshot 2025-01-07 at 21.53.49.png|1000]]
Tuttavia, le bolle non si muovono soltanto in base alle correnti dei venti, ma possono essere influenzate anche da altre bolle e dal giocatore. Infatti:
* Ogni bolla ha un campo di forza che respinge le altre per evitare che si sovrappongano.
* Il giocatore può spostare le bolle senza farle esplodere semplicemente avvicinandosi lentamente.

>[!note] Struttura a doppia hitbox
>
>Le bolle hanno due hitbox: una più grande e una più piccola.
>
>- L'hitbox più grande è la prima che va in contatto con il giocatore e permette di muovere la bolla nella direzione opposta al player.
>- Se il giocatore si muove molto velocemente, allora riuscirà a colpire la hitbox più interna (quella più piccola) attivando l'esplosione della bolla.
>
>![[bubblehitbox.png|300]]
