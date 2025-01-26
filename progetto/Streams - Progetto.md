---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-01-18T16:02
updated: 2025-01-20T20:01
---
In tutto il progetto, sono presenti 10 stream, che possono essere divisi in due categorie principali:

* **Ordinamento della lista di utenti**
* **Sincronizzazione tra modello e vista**

### Ordinamento della lista di utenti

`UserManagerModel` e`ScoreBoardOverlay` gli stream sono stati utilizzati per ordinare la lista di `User` in base a parametri specifici. Invece nell'interfaccia `levelImportMethods` gli stream sono utillizzati per ordinare i livelli presenti in una cartella.

Nella classe `UserManagerModel`, gli utenti sono ordinati in base all'ultimo tempo di selezione:

```java
public ArrayList<User> getUsers() {

  return (ArrayList<User>) users.values().stream()
          .sorted(Comparator.comparing(User::getLastSelectedTime).reversed())
          .collect(Collectors.toList());
}
```

Nella classe `ScoreBoard`, gli utenti sono ordinati in base al miglior punteggio: 

```java
public void updateUserScores() {  
	// sort users by best score    
    orderedUsers = (ArrayList<User>) usersManagerModel.getUsers().stream()  
            .sorted(Comparator.comparingInt(User::getBestScore).reversed())  
            .collect(Collectors.toList());  
}
```

Nell’interfaccia`LevelImportMethods`, i file presenti in `/levelMaps` sono ordinati lessicograficamente in base al nome del file:

```java
static BufferedImage[] GetAllLevels() {  
    URL url = LevelImportMethods.class.getResource("/levelMaps");  
    File file = null;  
  
    try {  
        file = new File(url.toURI());  
    } catch (URISyntaxException e) {  
        e.printStackTrace();  
    }  
  
    File[] files = file.listFiles();  
    File[] filesSorted = new File[files.length];  
  
    Arrays.stream(files).sorted(Comparator.comparing(File::getName))
					    .toList().toArray(filesSorted);
  
    BufferedImage[] levelImages = new BufferedImage[filesSorted.length];  
  
    for (int i = 0; i < levelImages.length; i++) {  
        try {  
            levelImages[i] = ImageIO.read(filesSorted[i]);  
        } catch (IOException e) {  
            e.printStackTrace();  
        }  
    }  
  
    return levelImages;  
}
```

### Sincronizzazione tra modello e vista

Nel gioco, ci sono molti oggetti come bolle, proiettili, ricompense, potenziamenti e punti. Per gestire questi oggetti, sono state create classi `manager` che si trovano sia nella **view** che nel **model**, ad esempio:
- `BubbleManagerModel` che si occupa della gestione di una lista di `BubbleModel` 
- `BubbleManagerView` che si occupa della gestione di una lista di `BubbleView` 

Gli stream sono utilizzati per controllare se nella lista di `bubleView` contenuta da `BubbleManagerView` ci sia un oggetto per ogni `bubbleModel` contenuto dalla lista in `BubbleManagerModel`. Se non esiste, viene creato un nuovo oggetto contenente il modello non associato.

Naturalmente questo non avviene sultano in per le bolle, ma è presente in tutti i manager che hanno sia una view che un model.

##### Tutti gli stream utilizzati

Inside the `PlayerBubblesManagerView` class:

```java
private void syncBubblesViewsWithModel() {  
    for (BubbleModel bm : playerBubblesManagerModel.getBubblesModels()) {  
        if (bubblesViews.stream().noneMatch(bv -> bv.getBubbleModel().equals(bm))) {
            switch (bm.getBubbleType()) {  
                case EMPTY_BUBBLE -> bubblesViews.add(new EmptyBubbleView(bm));  
                case ENEMY_BUBBLE -> bubblesViews.add(new EnemyBubbleView(bm));  
            }  
        }  
    }  
}
```


Inside the `SpecialBubblesManagerView` class:

```java
private void syncBubblesViewsWithModel() {  
    for (BubbleModel bm : bubblesManagerModel.getBubblesModels()) {  
    
        if (bubblesViews.stream().noneMatch(bv -> bv.getBubbleModel().equals(bm))) {
            switch (bm.getBubbleType()) {  
                case WATER_BUBBLE -> bubblesViews.add(new WaterBubbleView(bm));  
                case LIGHTNING_BUBBLE -> bubblesViews.add(new LightningBubbleView(bm)); 
            }  
        }  
    }  
}  
  

private void syncWaterFlowsViewsWithModel() {  
    for (WaterFlowModel wm : bubblesManagerModel.getWaterFlowsModels()) {  
    
        if (waterFlowsViews.stream().noneMatch(wv -> wv.getWaterFlowModel().equals(wm)))
            waterFlowsViews.add(new WaterFlowView(wm));  
    }  
}
```

Inside the `EnemyManagerView` class:

```java
private void syncEnemyViewsWithModel() {  
    for (var em : enemyManagerModel.getEnemiesModels()) {  
    
        if (enemiesViews.stream().noneMatch(ev -> ev.enemyModel.equals(em)))  
            switch (em.getEnemyType()) {  
                case MAITA -> enemiesViews.add(new EnemyView(em));  
                case ZEN_CHAN -> enemiesViews.add(new EnemyView(em));  
            }  
    }  
}
```

Inside the `ProjectileManagerView` class:

```java
private void syncProjectilesViewsWithModel() {  
  
    for (var p : projectileManagerModel.getProjectileModels()) {  
  
        if (projectilesViews.stream().noneMatch(pv -> pv.projectileModel.equals(p))) 
            switch (p.getType()) {  
                case MAITA_FIREBALL -> projectilesViews.add(new MaitaFireProjectileView(p));  
                case PLAYER_BUBBLE -> projectilesViews.add(new PlayerBubbleProjectileView(p));  
                case LIGHTNING -> projectilesViews.add(new LightingProjectileView(p));  
            }
```

Inside the `ItemManagerView` class:

```java
private void syncItemsViewsWithModel(){  
    for (var i : itemManagerModel.getItemsModels())  
        if (itemsViews.stream().noneMatch(iv -> iv.getItemModel().equals(i)))
        
            switch (i.getItemType()) {  
                case BUBBLE_REWARD -> itemsViews.add(new BubbleRewardView(i));  
                case POWER_UP -> itemsViews.add(new PowerUpView(i));  
            }  
}
```

Inside the `RewardPointsManagerView` class:

```java
private void syncPointsViewsWithModel() {  
    for (var p : RewardPointsManagerModel.getInstance().getPointsModelModelArray())  

        if (pointsViewArray.stream().noneMatch(pv -> pv.getPointsModel().equals(p))) 
            pointsViewArray.add(new PointsView(p));  
}
```