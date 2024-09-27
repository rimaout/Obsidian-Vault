---
type: Uni Note
class: 
academic year: 2023/2024
related: 
completed: false
created: 2024-09-18T10:49
updated: 2024-09-26T19:15
---
---
L'audio manager è la classe responsabile della gestione della riproduzione dei suoni all'interno del programma.

Per la riproduzione audio, ho deciso di utilizzare le classi `Clip` del pacchetto `javax.sound.sampled.Clip`. Questa classe consente di eseguire diverse azioni su file audio, tra cui:

- Riprodurre o fermare la riproduzione di un suono
- Gestire il volume
- Definire azioni da eseguire alla fine della riproduzione del suono

## Implementazione dell'Audio Manager

Ho suddiviso i tipi di audio in due categorie: canzoni ed effetti audio.

``` java
private Clip[] songs, soundEffects;  
private int currentSongID;
```

Ho deciso di dividerli in queste due categorie a causa delle loro caratteristiche diverse, infatti:

- Le canzoni non possono essere riprodotte contemporaneamente (a differenza degli effetti audio, che possono essere riprodotti contemporaneamente)
- Alla fine di una canzone, ne deve essere riprodotta automaticamente un'altra (a differenza degli effetti audio)

## Inizializzazione delle Clip

Una volta costruita la classe audio manager, converto i file `.wav`in oggetti `Clip`, e li salvo nelle corrispettive `arrayList.

```java
private void loadAudios() {
	// Load songs
    String[] songNames = { "song-intro-and-playing", "song-playing" };
    songs = new Clip[songNames.length];
    for (int i = 0; i < songNames.length; i++)
        songs[i] = GetAudio(songNames[i]);

    // Load sound effects
	String[] soundEffectNames = { "sfx-home", "sfx-jump", "sfx-player-death", "sfx-bubble-shoot" }
    soundEffects = new Clip[soundEffectNames.length];
    for (int i = 0; i < soundEffectNames.length; i++)
        soundEffects[i] = GetAudio(soundEffectNames[i]);
}

public static Clip GetAudio(String audioName) {  
    URL url = LoadSave.class.getResource("/audio/" + audioName + ".wav");  
    AudioInputStream audio;  
  
    try {  
        audio = AudioSystem.getAudioInputStream(url);  
        Clip clip = AudioSystem.getClip();  
        clip.open(audio);  
        return clip;  
    } catch (UnsupportedAudioFileException | IOException | LineUnavailableException e) {  
        e.printStackTrace();  
    }  
  
    return null;  
}
```

## Gestione delle Canzoni

Nel gioco ci sono due canzoni: la canzone iniziale (INTRO) che viene riprodotta solo all'inizio e un'altra canzone che si ripete per tutto il gioco (PLAYING).

Per fare ciò, all'inizio di una partita chiamo il seguente metodo:
```java
public void playIntroSong() {  
  
    currentSongID = INTO_AND_PLAYING_SONG;  
    setSongVolume();  
  
    // Create a listener to play the playing song after the intro song ends  
    LineListener listener = new LineListener() {  
        @Override  
        public void update(LineEvent event) {  
            if (event.getType() == LineEvent.Type.STOP) {  
                songs[currentSongID].removeLineListener(this);  
                playPlayingSong();  
            }  
        }  
    };  
  
    // Add the listener to the intro song  
    songs[currentSongID].addLineListener(listener);  
  
    // Start playing the intro song  
    songs[currentSongID].setFramePosition(0);  
    songs[currentSongID].start();  
}

public void playPlayingSong() {  
    stopSong();  
    currentSongID = PLAYING_SONG;  
    setSongVolume();  
    songs[currentSongID].setFramePosition(0);  
    songs[currentSongID].loop(Clip.LOOP_CONTINUOUSLY);  
}
```

Questo metodo, quando chiamato, inizia a riprodurre la canzone INTRO, ma aggiunge anche un listener che permette di riprodurre la canzone PLAYING in loop quando la canzone INTRO finisce.

---
## Gestione degli effetti Audio

