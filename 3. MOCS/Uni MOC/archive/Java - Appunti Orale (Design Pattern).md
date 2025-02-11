---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: false
created: 2025-02-10T20:17
updated: 2025-02-11T17:55
---
I design pattern sono soluzioni note di problemi specifici, che possono essere seguite passo passo.

Esistono tre categorie di design pattern:
- **Comportamentali:** riguardano al comportamento interni di degli oggetti
- **Creazionali:** riguardano meccanismi di creazione degli oggetti che aumentano la flessibilità e il riutilizzo del codice
- **Strutturali:** riguardano l'organizzazione delle classi


## Decorator

Il decorator è un design patter **strutturale** che permette di ampliare le funzionalità di una classe ma senza modificare il suo codice.

Si basa sull'idea di creare una classe wrapper (il decorator), che allo stesso tempo contiene come campo ed estende la classe che vuole decorare.

La classe wrapper deve implementare tutti gli stessi metodi della classe originale e per ognuno di questi chiama il metodo dell'oggetto originale, a cui poi è possibile aggiungere nuove funzionalità.

É anche possibile definire nuovi metodi non presenti nella classe originale.

![[Pasted image 20250211154953.png|900]]

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

## Command Callback



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



