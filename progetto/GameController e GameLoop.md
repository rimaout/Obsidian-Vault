---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-01-20T16:13
updated: 2025-01-20T20:01
---
## GameController e GameLoop

Il `GameController` è la prima classe inizializzata di tutto il gioco e da questa a cascata vengono inizializzate tutte le altre. Il suo scopo principale è quello di gestire il gameloop.

Il game loop è il cuore dell'app, responsabile di aggiornare e renderizzare il gioco a una frequenza costante. Per fare ciò, il `GameController` implementa l'interfaccia `Runnable`.

Il `GameController` contiene il metodo `run()` dell'interfaccia `Runnable`, che è chiamato automaticamente quando il gioco è avviato e continua a eseguire fino a quando il gioco non è terminato.

#### Run()

Questo metodo è il game loop vero e proprio e si occupa di chiamare a intervalli costanti i metodi `update()` e `render()`, che si occupano rispettivamente dell'aggiornamento e della renderizzazione di tutte le classi del gioco.

Il gameloop è basato su due concetti principali:

* **UPS (Updates Per Second)**: il numero di volte che il gioco viene aggiornato al secondo.
* **FPS (Frames Per Second)**: il numero di volte che il gioco viene renderizzato al secondo.

Il gameloop utilizza due variabili per tenere traccia del tempo:

* `timePerFrame`: il tempo necessario per renderizzare un frame.
* `timePerUpdate`: il tempo necessario per aggiornare il gioco.

Il gameloop esegue i seguenti passaggi:

1. Calcola il tempo trascorso dall'ultimo frame e dall'ultimo aggiornamento.
2. Aggiorna il gioco se il tempo trascorso dall'ultimo aggiornamento è maggiore o uguale a `timePerUpdate`.
3. Renderizza il gioco se il tempo trascorso dall'ultimo frame è maggiore o uguale a `timePerFrame`.
4. Calcola il numero di frame e aggiornamenti eseguiti al secondo.

Ecco il codice del gameloop:
```java
@Override
public void run() {
    double timePerFrame = 1000000000.0 / Constants.FPS_SET;
    long lastFrameTime = System.currentTimeMillis();
    int frames = 0;
    double deltaF = 0; // Delta Frame

    double timePerUpdate = 1000000000.0 / Constants.UPS_SET;
    long lastUpdateTime = System.nanoTime();
    int updates = 0;
    double deltaU = 0; // Delta Update

    // Game Loop
    while (true) {
        long currentTime = System.nanoTime();

        deltaU += (currentTime - lastUpdateTime) / timePerUpdate;
        deltaF += (currentTime - lastUpdateTime) / timePerFrame;
        lastUpdateTime = currentTime;

        if (deltaU >= 1) {
            update();
            updates++;
            deltaU--;
        }

        if (deltaF >= 1) {
            gamePanel.repaint();
            frames++;
            deltaF--;
        }

        // FPS | UPS Calculation
        if (System.currentTimeMillis() - lastFrameTime >= 1000) {
            lastFrameTime = System.currentTimeMillis();
            System.out.println("FPS: " + frames + " | UPS: " + updates);
            frames = 0;
            updates = 0;
        }
    }
}
```

#### Thread
Dope aver implementato l'interfaccia runnable e il metodo `run()` dobbiamo inserire questa class all'interno di un Thread che è eseguito in modo indipendente dal resto del gioco.

```java
public void startGameLoop() {  
    gameThread = new Thread(this);  
    gameThread.start();  
}
```