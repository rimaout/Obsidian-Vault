---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-01-20T18:47
updated: 2025-01-20T20:01
---
I design patter utilizzati in questo progetto sono tre:
- [#Observer/Observable](#Observer/Observable)
- [#Singleton](#Singleton)
- [#Flyweight](#Flyweight)

### Observer/Observable

L'Observer/Observable è un pattern di design comportamentale che consente di notificare gli oggetti interessati quando si verifica un evento specifico. Questo pattern è utile quando si hanno oggetti che devono essere aggiornati in base a cambiamenti in altri oggetti.

È particolarmente utile nel contesto dell'architettura MVC (Model-View-Controller), poiché consente di far comunicare il model con la view e il controller in modo asincrono e senza violare il principio di separazione delle responsabilità.

Il pattern di design Observer/Observable è stato adottato in due situazioni specifiche:

* Tra le classi `PlayingModel` e `PlayingView`
* Tra le classi `HurryUpManagerModel` e `HurryUpManagerView`

##### PlayingModel e PlayingView

In questo caso, `PlayingModel` estende `Observable`, e `PlayingView` implementa `Observer`.

Nel `GameController`, dove tutte e due le classi vengono inizializzate, chiamiamo `playingModel.addObserver(playingView);` per far osservare il `playingModel` dalla `playingView`.

Utilizziamo Observer/Observable per notificare alla `PlayingView` l'avvenimento di un reset per cambio di livello o un reset per restart della partita in `PlayingModel`.

Quando la view viene notificata, anche lei effettuerà un reset pertinente a quello effettuato dal model.

Nota: per reset si intende il cambio di alcuni campi allo stato di default.

Per fare ciò, quando vengono chiamati in `PlayingModel` i metodi `newLevelReset()` o `newGameReset()`, notifichiamo del cambiamento.

Codice di **PlayingModel**:

```java
public void nextLevelReset() {  
    // qui ci sono tutti i reset dei vari campi
  
    // notifica del cambiamento
    newLevelReset = true;  
    newPlayReset = false;  
    setChanged();  
    notifyObservers();  
}

public void newGameReset() {  
    // qui ci sono tutti i reset dei vari campi

    // notifica del cambiamento
    newPlayReset = true;  
    newLevelReset = false;  
    setChanged();  
    notifyObservers();  
}
```

Quando il model notifica la `PlayingView`, viene chiamato il metodo `update` che è implementato dall'interfaccia `Observer`. Questo metodo è stato implementato in modo tale che la view effettui lo stesso tipo di reset effettuato nel model.

Codice di **PlayingView**:

```java
@Override  
public void update(Observable o, Object arg) {  
    PlayingModel playingModel = (PlayingModel) o;  
  
    if (playingModel.isNewGameReset())  
        newGameReset();  
  
    if (playingModel.isNewLevelReset())  
        newLevelReset();  
}
```

##### HurryUpManagerModel e HurryUpManagerView

In questo caso, `HurryUpManagerModel` estende `Observable`, e `HurryUpManagerView` implementa `Observer`.

Nel `GameController`, dove tutte e due le classi vengono inizializzate, chiamiamo `hurryUpManagerModel.addObserver(HurryUpManagerView);` per far osservare il `hurryUpManagerModel` dalla `hurryUpManagerModel`.

Utilizziamo Observer/Observable per notificare alla `HurryUpManagerView` l'avvenimento di un reset in `hurryUpManagerModel`.

Codice di **HurryUpManagerModel**:

```java
public void reset() {  
    startHurryUpTimer = START_HURRY_UP_TIMER;  
    activateSkelMonstaTimer = ACTIVATE_SKEL_MONSTA_TIMER;  
  
    hurryUpActive = false;  
    skelMonsta.activateDespawn();  
  
    // notify observers  
    notifyObservers();  
    setChanged();  
}
```

Codice di **HurryUpManagerView**:

```java
@Override  
public void update(Observable o, Object arg) {  
    reset();  
} 
```

## Singleton

Il Singleton è un pattern creazionale che permette di garantire che una classe abbia solo un'istanza, mentre fornisce un punto di accesso globale a questa istanza.

**Aspetti positivi:** Oltre alla ad assicurare la creazione di una sola istanza della classe; un ulteriore vantaggio del Singleton è che consente l'accesso diretto all'istanza della classe attraverso il metodo `getInstance()` senza la necessità di recuperarla da altre classi che l'hanno creata. Ciò elimina la necessità di passare l'istanza della classe come parametro tra le diverse classi, semplificando la struttura del codice e migliorando la sua manutenzione.

**Aspetti negativi:** Tra gli aspetti negativi c'è il rischio di abusare del metodo `getInstance()`, creando più dipendenze tra classi di quelle di cui abbiamo veramente bisogno. Un altro aspetto negativo è che il metodo `getInstance()` non può avere parametri in input.

#### Utilizzo

Il pattern di design Singleton è stato adottato per tutte quelle classi che richiedono un'istanza unica e devono essere facilmente accessibili in tutto il progetto.

Le classi principali che hanno beneficiato di questo approccio sono:

* Tutti i manager di oggetti presenti nel package model, come ad esempio `BubbleManagerModel`, `EnemyManagerModel`, ecc. Queste classi devono essere instanziate una sola volta e sono utilizzate in diversi punti del progetto, anche nella view. L'utilizzo del metodo `getInstance` consente un accesso facile e efficiente a queste istanze.

Tuttavia, durante l'implementazione, ho incontrato un problema relativo all'utilizzo del `getInstance` su classi che richiedono costruttori con parametri in input. 

Per risolvere questo problema, ho adottato un approccio alternativo, consistente nell'implementare un costruttore senza parametri e successivamente chiamare un altro metodo che inizializza i campi necessari. Ad esempio:

```java
public class LevelTransitionModel {      
    private static LevelTransitionModel instance;  
    private PlayingModel playingModel;  
    // altri campi

    private LevelTransitionModel() {  
        playerModel = PlayerModel.getInstance();  
    }  
  
    public static LevelTransitionModel getInstance() {  
        if (instance == null)  
            instance = new LevelTransitionModel();  
        return instance;  
    }  
  
    public void initPlayingModel(PlayingModel playingModel) {  
        this.playingModel = playingModel;
```

## Flyweight

**Flyweight** è un modello di progettazione strutturale che consente di ridurre il consumo di memoria RAM, condividendo campi ad alto consumo di memoria comuni tra più oggetti.

Un esempio ovvio di questo design pattern sono le bolle. Ogni bolla che creiamo deve essere disegnata a schermo e per far ciò ha bisogno di una sprite (immagini utilizzate per l'animazione). Inoltre, in un livello potrebbero essere presenti contemporaneamente tantissime bolle, e per motivi di prestazioni, le bolle una volta fatte esplodere non vengono cancellate dalla lista, ma semplicemente non vengono più aggiornate o disegnate. La loro cancellazione avviene soltanto a fine livello.

Questo significa che in ogni livello potrebbero contenere anche 1000 bolle, e considerando che la sprite delle bolle ha una dimensione di `10KB`, lo spazio occupato da 1000 bolle sarebbe di circa `10 megabyte`.

Per risolvere questo problema, invece di salvare la sprite in ogni bolla, possiamo inserirla nel `bubbleManagerView` come campo e ogni volta che una bolla deve essere disegnata, possiamo usare un getter in `bubbleManagerView` per accedere all'immagine della bolla. Questo approccio consente di ridurre il consumo di memoria RAM, ma ha anche degli aspetti negativi, come ad esempio un aumento leggermente maggiore dell'utilizzo del processore.

Esempio del draw di una bolla:

```java
public void draw(Graphics g) {  
    g.drawImage(bubblesManagerView.getBubbleSprites()[stateIndex][animationIndex], ...);  
}
```

Il pattern di design Flyweight non viene applicato soltanto per le sprite delle bolle, ma viene utilizzato anche per altri oggetti nel gioco. Ecco un elenco degli oggetti che utilizzano questo pattern:

| Oggetto     | Campi Utilizzati     |
| ----------- | -------------------- |
| Bubbles     | Sprite, Mappa, Venti |
| Enemies     | Sprite, Mappa        |
| Projectiles | Sprite, Mappa        |
| Items       | Sprite, Mappa        |
| Points      | Sprite               |
