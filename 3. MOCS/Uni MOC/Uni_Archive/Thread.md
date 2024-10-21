---
type: Uni Note
class:
  - "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related: 
completed: false
created: 2024-10-20T16:57
updated: 2024-10-20T20:21
---
>[!abstract] Index
>1. 

>[!abstract] Related
>- 

---
## Introduzione

Per ora abbiamo visto che ci sono più processi che si alternano lo stato di esecuzione sul computer, però non è sempre così, alcune applicazioni sono organizzate in modo parallelo e non perché lo decide il SO ma perché lo ha deciso il programmatore dell’applicazione, ogni esecuzione dell’applicazione si chiama Thread.

Ad esempio per un’applicazione grafica possiamo avere:
- Un thread per gli input del mouse
- Uno per disegnare su schermo
- Un altro per effettuare i calcoli richiesti

>**oss:** Ricordiamo che di per sé è un **processo unico** ma ci sono **più threads**.

>[!note] Risorse
>Diversi threads di uno stesso processo condividono tutte le risorse del processo tranne **lo stack delle chiamate** e **il processore**.
>
>Il resto delle risorse è completamente condiviso, per **esempio**: 
>- se un thread acquisisce un dispositivo di I/O (un file), è come se l’avesse acquisito l’intero processo quindi, anche tutti gli altri thread di quel processo vedono quel file.
>
>>**oss:** se non ho abbastanza processori non è detto che tutti i thread vadano in esecuzione

Il concetto di processo come visto prima ha 2 caratteristiche principale:
- **Gestione delle risorse** che per quanto riguarda i processi vanno visti come blocco unico
- **Scheduling** ovvero che i processi possono contenere diverse _tracce_ ovvero diversi _threads_ Nel caso di più threads vanno trattati in maniera diversa.

>[!done] Vantaggio dei Thread
>
>I Thread rispetto hai processi sono più efficienti, è inoltre più semplice crearli, terminarli e fare lo switching.
>
>Ogni processo viene creato con un thread al suo interno, dopo il programmatore può utilizzare questo thread per 
>
>Dopodiché è possibile fare le seguenti operazioni:
>- **Spawn:** permette creare altri thread con una chiamata di sistema (più leggera del fork dato che ha meno istruzioni da fare, non crea tutti gli spazi necessari per un processo)
>- **Block:** che permette di interrompere l'esecuzione del thread (non per I/O ad esmpio perchè deve aspettare un altro thread)
>- **Unblock:** rimuove il blocco a un thread
>- **Finish:** si può eliminare un thread
>
>Ricordiamo che tutte queste operazioni vengono svolte all’interno dello stesso processo e che un processo deve sempre avere almeno un thread.

---
## Rappresentazione dei Threads

>[!column|flex] 
>
>>[!NOTE|clean no-title]
>>
>>![[Pasted image 20241020193316.png]]
>
>>[!NOTE|clean no-title]
>>
>>![[Pasted image 20241020193412.png]]

Quindi in un sistema a singolo thread è gestito come abbiamo visto fino ad adesso con un PCB per ogni processo e i 2 stack.

Su un sistema multithread abbiamo un PCB del processo, la _User Address Space_ che è la parte in comune fra tutti i thread, quindi variabili globali ecc.., e per ogni thread la gestione di quel thread quindi un **Thread Control Block** che serve a gestire lo scheduling fra questi e poi due stack separati per ogni thread, uno utente e uno kernel mode.

---
## ULT vs KLT

**ULT:** User Level Thread
**KLT:** Kernel Level Thread

![[Pasted image 20241020202110.png|600]]