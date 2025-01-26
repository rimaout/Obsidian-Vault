---
type: Programming Note
programming language: "[Java MOC](Java%20MOC.md)"
related: 
completed: false
created: 2024-07-17T15:34
updated: 2025-01-20T20:01
---

## Java Swing

In questo progetto, abbiamo utilizzato Java Swing per creare l'interfaccia grafica dell'applicazione. Java Swing offre una vasta gamma di componenti per creare interfacce utente intuitive e personalizzabili.

**Componenti Utilizzati**

Per creare una finestra funzionante con Java Swing, abbiamo bisogno di due componenti principali:

* `JFrame`: si occupa della generazione del frame della finestra.
* `JPanel`: si occupa della generazione dell' "immagine" contenuta del frame.

Nel nostro progetto, abbiamo utilizzato solo questi due componenti, poiché non erano necessari altri componenti come `JButton`, `JTextField` o `JTable`.

![500](Pasted%20image%2020240718122039.png)

### JFrame

La classe `GameFrame` estende `JFrame` e si occupa di inizializzare le caratteristiche del frame della finestra. Le operazioni essenziali che effettuiamo sono:
- Impostare il titolo della finestra
- Impostare la dimensione della finestra
- Aggiungere il pannello di gioco
- Impostare la posizione della finestra sullo schermo

Le operazioni "superflue" sono:
- Impostare l'icona della finestra
- Personalizzare la barra dei titoli su macOS

Ecco il codice della classe `GameFrame`:
```java
public class GameFrame extends JFrame {  
  
  public GameFrame(GamePanel gamePanel){  
  
    setTitle("BubbleBobble"); // Set the title of the window  
    setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE); 
    add(gamePanel);  
  
    setResizable(false);  
    pack(); // Adjust the size of the window to fit the preferred size 
    setLocationRelativeTo(null); // Center the window on the screen  

    setGameIcon();  
    macOSTitleBarCustomizations(); 
	
    setVisible(true);  
    createWindowFocusListener(gamePanel);  
  }  
  
  private void createWindowFocusListener(GamePanel gamePanel){  
    addWindowFocusListener(new WindowFocusListener() {  
      @Override  
      public void windowGainedFocus(WindowEvent e) {  
        // empty method (if focus is gained do nothing)  
      }  
  
      @Override  
      public void windowLostFocus(WindowEvent e) {  
        gamePanel.getGameController().windowFocusLost();  
      }  
    });  
  } 
  
  private void setGameIcon(){  
    Image icon = new ImageIcon(GAME_ICON).getImage();  
    setIconImage(icon); // Set the icon of the window  

    // set taskbar icon
    try {  
      Taskbar.getTaskbar().setIconImage(icon);  
    } catch (UnsupportedOperationException e) {  
      System.out.println("TaskBar not supported on Windows!");  
    }  
  }  
  
  private void macOSTitleBarCustomizations() {    
    if (System.getProperty("os.name").toLowerCase().contains("mac")) {  
      getRootPane().putClientProperty("apple.awt.fullWindowContent", true);  
      getRootPane().putClientProperty("apple.awt.transparentTitleBar", true);  
      getRootPane().putClientProperty("apple.awt.windowTitleVisible", false);  
    } else {  
      System.out.println("macOS customizations are not applied as the current OS is not macOS.");  
    }  
  }  
}
```

### JPanel

Il pannello di gioco è un componente fondamentale dell'applicazione. La classe `GamePanel` estende `JPanel` e si occupa di gestire l'interfaccia grafica del gioco.

Il costruttore della classe `GamePanel` accetta un oggetto `GameController` come parametro. Questo oggetto è responsabile della gestione degli eventi, ed in particolare del **gameLoop** per la generazione degli FPS, oltre a questo inizializza gli `InputListener`.

```java
public GamePanel(GameController gameController) {  
    this.gameController = gameController;  
    setBackground(Color.BLACK);  
    setPanelSize();  
  
    // Input Listeners  
    addKeyListener(new KeyBoardInputs(this));  
    addMouseListener(new MouseKeyInputs(this));  
    addMouseMotionListener(new MouseMotionInputs(this));  
}
```

La dimensione del pannello è impostata utilizzando la classe `Dimension`. La larghezza e l'altezza del pannello sono definite dalle costanti `Constants.GAME_WIDTH` e `Constants.GAME_HEIGHT`.

```java
private void setPanelSize() {  
    Dimension size = new Dimension(Constants.GAME_WIDTH, Constants.GAME_HEIGHT);  
    setPreferredSize(size);  
}
```

Il metodo `paintComponent` è responsabile del rendering dell'interfaccia grafica del gioco. Questo metodo è chiamato automaticamente dal sistema di rendering di Java.

```java
public void paintComponent(Graphics g) {  
    Toolkit.getDefaultToolkit().sync();
    super.paintComponent(g);
    
    gameController.render(g);  
}
```
