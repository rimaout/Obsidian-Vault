---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-01-18T12:28
updated: 2025-01-20T20:01
---
All'avvio del gioco, verrà richiesto di selezionare (o creare) un profilo utente che verrà utilizzato per salvare i progressi effettuati dal giocatore. In particolare, i dati utilizzati sono:
- Numero di partite giocate
- Numero di vittorie
- Informazioni riguardanti l'orario e la data dell'ultima partita giocata

Tutte queste informazioni vengono gestite da una classe `User` che permette di salvare i dati su disco implementando l'interfaccia `Serializable`.

## Salvataggio e Lettura

Nella classe `User` sono presenti due metodi `save()` e `read()` che rispettivamente permettono di salvare su disco i cambiamenti effettuati e di leggere i file utente per trasformarli in un oggetto `User`.

```java
public void save(String fileName) {  
    File directory = new File("res/users-data");  
    if (!directory.exists()) {  
        directory.mkdirs();  
    }  
  
    try {  
        FileOutputStream fos = new FileOutputStream(directory + File.separator + fileName);  
        ObjectOutputStream oos = new ObjectOutputStream(fos);  
  
        oos.writeObject(name);  
        oos.writeObject(profilePictureIndex);  
        oos.writeObject(bestScore);  
        oos.writeObject(playedGames);  
        oos.writeObject(wonGames);  
  
        oos.close();  
        fos.close();  
    } catch (IOException e) {  
        e.printStackTrace();  
    }  
}  
```

```java
public static User read(String fileName) {  
    try {  
        // Apri il file  
        FileInputStream fis = new FileInputStream(fileName);  
        ObjectInputStream ois = new ObjectInputStream(fis);  
  
        // Leggi e Casting  
        String name = (String) ois.readObject();  
        int profilePictureIndex = (int) ois.readObject();  
        int bestScore = (int) ois.readObject();  
        int playedGames = (int) ois.readObject();  
        int wonGames = (int) ois.readObject();  
  
        // Crea l'utente  
        User user = new User(name, profilePictureIndex);  
        user.bestScore = bestScore;  
        user.playedGames = playedGames;  
        user.wonGames = wonGames;  
  
        ois.close();  
  
        return user;  
    }  
    catch (ClassNotFoundException | IOException e) {  
        e.printStackTrace();  
        return null;  
    }  
}
```

## User Manager

La classe `UserManager` è utilizzata per la gestione dell'utente. In particolare, è usata per:

- Leggere tutti i file utente e trasformarli in oggetti `User` grazie all'interfaccia `Serializable`
- Creazione di nuovi utenti
- Selezione di un utente

Questa classe contiene il campo `selectedUser` che contiene l'utente attualmente attivo. `UserManager` è utilizzato dalle altre classi dell'app come interfaccia per accedere all'utente selezionato.

![usermanagerviewexample](usermanagerviewexample.png)

