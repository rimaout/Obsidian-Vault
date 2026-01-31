---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: false
created: 2025-02-10T20:17
updated: 2026-01-31T13:32
---
I design pattern sono soluzioni note di problemi specifici, che possono essere seguite passo passo.

Esistono tre categorie di design pattern:
- **Comportamentali:** riguardano al comportamento interni di degli oggetti
- **Creazionali:** riguardano meccanismi di creazione degli oggetti che aumentano la flessibilità e il riutilizzo del codice
- **Strutturali:** riguardano l'organizzazione delle classi

## Observer

Design pattern **strutturale** dove gli oggetti sono divisi in:

- Gli osservabili estendono la classe **Observable** 
- Gli osservatori che implementano l’interfaccia **Observer**

Ogni osservabile ha una lista dei suoi osservatori ai quali invia una notifica ad ogni suo cambio di stato tramite il metodo **notifyObserver**. Gli Observer hanno un metodo **update** che viene chiamato quando ricevono una notifica dai loro observable.

## Iterator

Viene utilizzato per accedere agli elementi di una collezione in sequenza senza esporre la struttura sottostante alla collezione stessa. Tramite questo pattern separiamo la logica della collezione dall’iterazione in modo da nascondere i dettagli interni.

## Template Method

Il template method serve a permettere a delle sottoclassi di una classe astratta di re-implementare solo alcune parti di un algoritmo favorendo quindi la personalizzazione soltanto di alcuni passaggi. I suoi componenti sono quindi:

- **Template Method**: Il metodo che definisce la logica base da non modificare, di solito è final per non permettere modifiche.
- **Metodi astratti**: Sono i metodi che verrano ridefiniti dalle sottoclassi, quindi i passi personalizzabili visti primi.
- **Metodi Concreti**: Metodi già implementati nella classe base ma anch’essi non modificabili. Quindi una classe astratta definisce il template method che chiama una serie di metodi astratti che verrano implementati dalle sottoclassi a modo loro.

## Callback pattern

Il callback pattern consiste nell’invocare una funzione quando un’operazione è terminata, un callback non è altro che una funzione passata come parametro ad un’altra funzione, quando la prima termina allora viene chiamato il callback.

In Java le funzioni di callback vengono implementate tramite interfacce funzionali.

>[!example]- Esempio
>
>```java
>@FunctionalInterface
>public interface Callback {
>	void execute();
>}
> 
>class Task { 
>	public void execute(Callback callback) { 
>		System.out.println("Eseguendo un'operazione lunga...");
>		try { 
>			Thread.sleep(2000); 
>		} catch (InterruptedException e) {
>			e.printStackTrace();
>		}
>		callback.onComplete();
>	}
>}
> 
>public class CallbackExample {
>	public static void main(String[] args) {
>		Task task = new Task();
>		task.execute(() -> System.out.println("Operazione completata!"));
>	}
>}
>```

In questo modo non ci interessa dell’operazione che svolge la classe Task, ma sappiamo che una volta finita stamperà a schermo “Operazione completata!“.

## Command

Questo design pattern serve a incapsulare una richiesta o un’azione di un oggetto, in questo modo la rendiamo modulare e possiamo associarla ad altri oggetti. Gli obiettivi principali infatti sono:

- Disaccoppiamento tra mittente e ricevente: chi richiede l’esecuzione non è interessato a chi la svolgerà.
- Incapsulamento della richiesta: Ogni comando rappresenta una richiesta.

Abbiamo bisogno di:

- Una classe astratta o interfaccia command che dichiara il metodo execute().
- Una classe concreta che implementa un’azione specifica per il comando.
- Receiver: ovvero l’oggetto che riceve l’azione quando viene chiamato il comando.
- Invoker: L’oggetto che invoca il comando.
- Client: L’oggetto che crea il comando e lo assegna ad un invoker

Quindi la classe client creerà il _ricevitore_, varie classi _command_ per i comandi e un _invoker_ al quale passerà il giusto comando da invocare, tramite un metodo dell’invoker chiamerà il metodo che gli è assegnato in quel momento.

## Strategy

È un design patter **comportamentale** che permette di definire delle superclassi dove alcuni dei comportamenti non implementati direttamente attraverso dei metodi ma sono delegati a delle interfacce funzionali.

Per ognuna di queste interfacce è possibile creare diverse implementazioni con comportamenti diversi che chiameremo famiglie di algoritmi.

Le sotto classi quando definite potranno scegliere attraverso il costruttore della `superclasse` quali comportamenti utilizzare per implementare le interfacce.

![[Pasted image 20250211162038.png|900]]

**Esempio Sotto Classe:**

```java
public class AnatraDomestica extends Anatra {
	public AnatraDomestica() { 
		compVolo = new VoloConAli(); compStarnazzo = new Starnazzo(); 
	}
}
```

## SimpleFactory

Se dobbiamo creare un oggetto di una classe con diverse sottoclassi potrebbe capitare di non sapere fino a tempo di esecuzione quale sottoclasse istanziare.

In questo caso possiamo usufruire del **Factory** un design patter **creazionale** che delega il compito di creare il giusto oggetto ad una nuova classe Factory.

All interno abbiamo un metodo statico che si occupa di creare e ritornare l'istanza ad oggetto della giusta sotto classe. Questa scelte è effettuata attraverso un logica interna che è influenzata da un input.

## Factory

Problema del simple factory è che se aggiungiamo una nuova sotto classe dobbiamo cambiare il metodo della classe factory che si occupa della creazione della classe.

Per risolvere questo problema possiamo definire un interfaccia che si occupa della creazione dell'oggetto e ogni sotto classe può implementarla a modo suo.
## Builder

È un design pattern **creazionale** utilizzato per la costruzione di oggetti complessi aventi molti parametri opzionali. 

Un opzione sarebbe creare tanti costruttori ma questa chiaramente non è una buona opzione.

Per risolvere possiamo:
- La classe Builder generica è una classe statica nidificata all'interno della classe che vogliamo costruire.
- Builder gli stessi attributi obbligatori e opzionali della classe generica.
- Il costruttore (della classe Builder) accetta gli attributi obbligatori come parametri.
- La classe Builder fornisce metodi per impostare gli attributi opzionali. Questi metodi restituiscono l'istanza corrente del Builder, attraverso `this`, per consentire la concatenazione dei metodi.
- Infine, la classe Builder fornisce un metodo build() che restituisce un'istanza della classe generica con gli attributi impostati.

Per creare un oggetto ci basta creare il builder e chiamare su di esso i metodi per inizializzare i campi, una volta finito possiamo usare il metodo `buil()`che ritornerà l'oggetto.

## Singleton

Design patter **creazionale** che rende possibile istanziare una classe una sola volta:

- nella classe creiamo statico `instance` del tipo della classe.
- Rendiamo il costruttore `private`.
- Creiamo un metodo statico `getInstance()` che ritorna l'istanza dell’oggetto, il metodo crea una nuova istanza dell’oggetto se l'istanza è `null` altrimenti ritorna l’istanza già esistente.

## Decorator

Il decorator è un design patter **strutturale** che permette di ampliare le funzionalità di una classe ma senza modificare il suo codice.

Si basa sull'idea di creare una classe wrapper (il decorator), che allo stesso tempo contiene come campo ed estende la classe che vuole decorare.

La classe wrapper deve implementare tutti gli stessi metodi della classe originale e per ognuno di questi chiama il metodo dell'oggetto originale, a cui poi è possibile aggiungere nuove funzionalità.

É anche possibile definire nuovi metodi non presenti nella classe originale.

![[Pasted image 20250211154953.png|900]]
