---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related: 
completed: false
created: 2025-01-06T21:24
updated: 2025-01-17T16:54
---
---
## Livelli

I **livelli** sono un elemento fondamentale del gioco. Ogni livello è composto da una serie di elementi, tra cui la mappa, le tile, i nemici e le bolle. 

A livelli pratico i livelli sono oggetti rappresentati da oggetti composti da cinque campi specifici: l'immagine della mappa, un array 2D di interi che rappresenta il tipo e la posizione delle tile, un array 2D di direzioni utilizzato per ricreare le correnti dei venti, un generatore di bolle che gestisce la posizione e il tipo di bolle speciali da generare, e una lista di nemici.

```java
public class Level {  
  
    private BufferedImage levelMap;
    private int[][] levelTileData;
    private Direction[][] windDirectionData;
    private BubbleGenerator bubbleGenerator;
    private ArrayList<EnemyModel> Enemies;
    
    //methods...
}
```

Come vedremo tutte queste informazioni sono inizialmente estrapolate dalla `levelMap`.

### Level Map

La mappa di livello è un'immagine composta da 32x38 pixel, ognuno dei quali rappresenta una tile del livello. 

Le informazioni di ogni tile sono codificate nell'immagine `levelMap` utilizzando i canali RGB dei pixel. Il canale rosso è utilizzato per codificare il tipo di tile, il canale verde è utilizzato per codificare il tipo di nemico e il canale blu è utilizzato per codificare la direzione dei venti.

Inoltre, il primo pixel in alto a sinistra di ogni livello contiene informazioni riguardanti il `BubbleGenerator`, una classe che si occupa di generare le bolle.
![[Screenshot 2025-01-07 at 10.10.59.png.png|1000]]
A sinistra abbiamo la `levelMap` a destra il risultato a schermo.

### Tiles

Ogni livello è composto da campo chiamato `levelTileData` ovvero un array bidimensionale di interi (32x38) a cuoi ogni intero è associata una tile. In particolare all'intero 1 è associata la tile del primo livello, all'intero due la tile del secondo livello e cosi via per tutti i restanti livelli.

Questa informazione non viene utilizzata soltanto per disegnare la mappa a schermo ma anche per calcolare le collisioni delle entità con la mappa, infatti qualsiasi tile con valore intero compreso tra 1 e 150 è considerata solida.

L'array 2D di interi che rappresenta le tile è "generato" dalla `LevelMap` image attraverso il seguente metodo:

```java
static int[][] GetLevelTilesData(BufferedImage img) {  
  
    int levelData[][] = new int[Constants.TILES_IN_HEIGHT][Constants.TILES_IN_WIDTH];  
  
    for(int x = 0; x < img.getHeight(); x++)  
        for (int y = 0; y < img.getWidth(); y++) {  
  
            Color color = new Color(img.getRGB(y, x));  
            int red = color.getRed();  
            if (red >= 150)  
                red = 0;  
  
            levelData[x][y] = red;  
        }  
    return levelData;  
}
```

Questo metodo fa un parsing dell'immagine pixel per pixel e controlla il valore del canale rosso di ogni pixel per ottenere l'intero che rappresenta la tile nell'array 2D.

### Direzione dei venti

La classe `level` al suo interno contiene campo di nome `windDirectionData` ovvero un array dimensionale (32x38) di "direzioni", dove ogni elemento rappresenta la direzione del vento della tile associata.

>[!info] Direction
>Direction non è altro che un enum definita in questo modo:
>
>```java
>enum Direction {
>	LEFT, RIGHT, UP, DOWN, NONE;
>}
>```

Questa informazione è utilizzata dalle bolle per capire in che direzione devono muoversi, infatti la bolla può utilizzare la sue coordinate `x`, `y` per calcolare le calcolare su che tile si trova, facendo ciò può accedere all'array `windDirectionData` e prendere la direzione in muoversi da questo array.

L'array 2D di direzioni è "generato" dalla `LevelMap` image attraverso il seguente metodo:

```java
static Direction[][] GetWindsDirectionsData(BufferedImage img) {  
  
    Direction[][] windDirectionData = new Constants.Direction[TILES_IN_HEIGHT][TILES_IN_WIDTH];  
  
    for(int x = 0; x < img.getHeight(); x++)  
        for (int y = 0; y < img.getWidth(); y++) {  
  
            Color color = new Color(img.getRGB(y, x));  
            int blue = color.getBlue();  
  
            if (blue >= 100)  
                blue -= 100;  
  
            Direction direction;  
  
            switch (blue) {  
                case 1 -> direction  = Direction.LEFT;  
                case 2 -> direction  = Direction.RIGHT;  
                case 3 -> direction  = Direction.UP;  
                case 4 -> direction  = Direction.DOWN;  
                default -> direction = Direction.NONE;  
            }  
  
            windDirectionData[x][y] = direction;  
        }  
  
    return windDirectionData;  
}
```

Utilizziamo il colore blue dei pixel dell'immagine per codificare l'informazione, dove se il valore è:
- `0` o `100`: nessun vento
- `1` o `101`: vento verso sinistra
- `2` o `102`: vento verso destra
- `3` o `103`: vento verso l'alto
- `4` o `104`: vento verso il basso

Combinando i venti delle singole tile è possibile creare delle correnti d'aria per gestire i movimenti delle bolle e portarle nei punti di accumulazione.
![[Screenshot 2025-01-07 at 21.53.49.png|1000]]

### Bubble Generator

Ogni livello contiene un oggetto `BubbleGenerator`. Questa classe si occupa di generare le bolle speciali, come le `WaterBubble` e le `LightingBubble`, che possono spawnare in due zone diverse, dalla parte alta o dalla parte bassa.

Le informazioni relative al `BubbleGenerator` di ogni livello sono codificate nel canale verde del primo pixel in alto a sinistra della `levelMap`. Il valore di questo pixel determina il tipo di bolle da generaMa re e la loro posizione:

* 101: verranno generate `WaterBubble` nella parte alta della mappa
* 102: verranno generate `WaterBubble` nella parte bassa della mappa
* 103: verranno generate `LightingBubble` nella parte alta della mappa
* 104: verranno generate `LightingBubble` nella parte bassa della mappa
* qualsiasi altro valore indica che non ci sono generatori di bolle nel livello

Queste informazioni vengono estrapolate dall'immagine `levelMap` attraverso il seguente metodo:
```java
static BubbleGenerator GetBubbleGenerator(BufferedImage img) {  
  
    Color color = new Color(img.getRGB(0, 0));  
    int green = color.getGreen();  
    BubbleGenerator bubbleGenerator;  
  
    switch (green) {  
        case 101 -> bubbleGenerator = new BubbleGenerator(WATER_BUBBLE, TOP);  
        case 102 -> bubbleGenerator = new BubbleGenerator(WATER_BUBBLE, BOTTOM);  
        case 103 -> bubbleGenerator = new BubbleGenerator(LIGHTNING_BUBBLE, TOP);  
        case 104 -> bubbleGenerator = new BubbleGenerator(LIGHTNING_BUBBLE, BOTTOM);  
        default  -> bubbleGenerator = new BubbleGenerator(NONE, NONE);  
    }  
  
    return bubbleGenerator;  
}
```

### Nemici

Ogni livello contiene una lista di nemici che verrà utilizzata dall'`EnemyManager` per la gestione di questi ultimi. La creazione di questa lista avviene in base alle informazioni estrapolate dalla `levelMap` image, dove ogni pixel rappresenta una tile della mappa.

Il canale verde dei valori RGB dei pixel viene utilizzato per indicare la tipologia di nemico che appartiene alla tile associata a quel pixel. In particolare, se il canale verde assume i seguenti valori:
- 1, allora su quella tile verrà generato un nemico `ZenChan` con direzione iniziale sinistra.
- 2, allora su quella tile verrà generato un nemico `ZenChan` con direzione iniziale destra.
- 3, allora su quella tile verrà generato un nemico `Maita` con direzione iniziale sinistra.
- 4, allora su quella tile verrà generato un nemico `Maita` con direzione iniziale destra.

Queste informazioni vengono estrapolate dall'immagine attraverso un metodo specifico.

```java
static ArrayList<EnemyModel> GetEnemies(BufferedImage img) {  
  
    ArrayList<EnemyModel> list = new ArrayList<>();  
  
    for(int x = 0; x < img.getHeight(); x++)  
        for (int y = 0; y < img.getWidth(); y++) {  
  
            Color color = new Color(img.getRGB(y, x));  
            int green = color.getGreen();  
  
            switch (green) {  
                case 1 -> list.add(new ZenChanModel(y * TILES_SIZE, x * TILES_SIZE, LEFT));  
                case 2 -> list.add(new ZenChanModel(y * TILES_SIZE, x * TILES_SIZE, RIGHT));  
                case 3 -> list.add(new MaitaModel(y * TILES_SIZE, x * TILES_SIZE, LEFT));  
                case 4 -> list.add(new MaitaModel(y * TILES_SIZE, x * TILES_SIZE, RIGHT));  
            }  
        }  
    return list;  
}
```