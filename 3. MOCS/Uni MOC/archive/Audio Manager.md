---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-01-18T14:09
updated: 2025-01-18T15:55
---
L'`AudioManager` è una classe della `view` che si occupa della gestione degli audio, in particolare delle canzoni e degli effetti sonori.

I suoni sono salvati in file di tipo `wav` e utilizzano la classe `Clip` per la riproduzione dei suoni. Questi file, essendo particolarmente pesanti, vengono processati soltanto una volta all'avvio del gioco e poi, ad ogni riproduzione, viene riprodotta la clip dello specifico suono presente in una lista.

## Inizializzazione

Durante l'inizializzazione della classe, chiamiamo il metodo `loadAudios()` che, attraverso la classe `Clip`, converte i file audio in oggetti che possono riprodurre dei suoni.

```java
private void loadAudios() {  
    // Carica le canzoni  
    String[] songNames = {"song-intro-and-playing", "song-playing"};  
    songs = new Clip[songNames.length];  
    
    for (int i = 0; i < songNames.length; i++)  
        songs[i] = GetAudio(songNames[i]);  
  
    // Carica gli effetti sonori  
    String[] soundEffectNames = {"sfx-home", "sfx-jump", ..., "sfx-hurry-up"};  
    soundEffects = new Clip[soundEffectNames.length];  
    
    for (int i = 0; i < soundEffectNames.length; i++)  
        soundEffects[i] = GetAudio(soundEffectNames[i]);  
  
    setSoundEffectVolume();  
}
```

## Canzoni

Nel gioco ci sono due canzoni: **intro-song** e **playing-song**. L'`intro-song` viene riprodotta all'inizio della partita e, alla sua fine, viene automaticamente riprodotta la `playing-song`. Quest'ultima viene riprodotta in loop, ovvero viene riprodotta da capo ogni volta che finisce.

Questi automatismi sono ottenuti attraverso degli `action-listener` che permettono di eseguire del codice specifico quando avviene un determinato evento. In questo caso, quando l'`intro-song` termina, riproduciamo la `playing-song` in loop.

```java
public void playIntroSong() {  
    currentSongID = INTO_AND_PLAYING_SONG;  
    setSongVolume();  
  
    // Crea un listener per riprodurre la playing song dopo la fine dell'intro song  
    LineListener listener = new LineListener() {  
        @Override  
        public void update(LineEvent event) {  
            if (event.getType() == LineEvent.Type.STOP) {  
                songs[currentSongID].removeLineListener(this);  
                playPlayingSong();  
            }  
        }  
    };  
  
    // Aggiunge il listener alla intro song  
    songs[currentSongID].addLineListener(listener);  
  
    // Inizia a riprodurre la intro song  
    songs[currentSongID].setFramePosition(0);
```

## Effetti Sonori

| Suono                   | Descrizione                                     |
| ----------------------- | ----------------------------------------------- |
| `sfx-jump`              | Suono del salto del player                      |
| `sfx-player-death`      | Suono della morte del player                    |
| `sfx-bubble-shoot`      | Suono dell'attacco del player                   |
| `sfx-enemy-bubble-pop`  | Suono della enemy bubble che espode             |
| `sfx-water-flow`        | Suono della bolla d'acqua che esplode            |
| `sfx-lightning`         | Suono della bolla lampo che esplode              |
| `sfx-reward-collected`  | Suono riprodotto quando si raccoglie un reward  |
| `sfx-powerup-collected` | Suono riprodotto quando si raccoglie un powerUp |
| `sfx-hurry-up`          | Suono riprodotto quando inizia l'evento hurryUp |
| `sfx-game-over`         | Suono riprodotto quando si perde la partita     |
| `sfx-game-completed`    | Suono riprodotto quando si vince il gioco       |
| `sfx-home`              | Suono riprodotto quando si avvia l'app          |

Ogni suono ha un id specifico e possiamo riprodurre i suoni attraverso questo metodo:

```java
public void playSoundEffect(int soundEffectID) {  
    soundEffects[soundEffectID].start();  
```
