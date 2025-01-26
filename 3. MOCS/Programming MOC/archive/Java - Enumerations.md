---
type: Programming Note
programming language: "[[Java MOC]]"
related:
  - "[[Metodologie di Programmazione (class)]]"
completed: true
created: 2024-06-17T11:22
updated: 2025-01-26T12:47
---
>[!abstract] Index
>1. [[#Introduzione]]
>2. [[#Campi, Metodi, e Costruttori]]
>3. [[#Metodi Polimorfici]]
>4. [[#Interfacce ed Enum]]

>[!abstract] Related
>- [[Java MOC]]
>- [](Java%20MOC.md)e di Programmazione (class)]]

---
## Introduzione

In Java, le enum sono un tipo speciale di classe che rappresenta un insieme di costanti. Sono utili quando si desidera lavorare con un gruppo di valori ben definiti e limitati.

>[!note] Esempio
>```java
>public enum GiorniDellaSettimana {     
>	LUNEDI,     
>	MARTEDI,     
>	MERCOLEDI,     
>	GIOVEDI,     
>	VENERDI,     
>	SABATO,     
>	DOMENICA 
>}
>```
>
>In questo esempio, `GiorniDellaSettimana` è una enum che rappresenta i sette giorni della settimana. Ogni giorno è definito come una costante all'interno della enum.
>
>Puoi utilizzare le enum come qualsiasi altro tipo di dato in Java. Ad esempio, puoi dichiarare una variabile di tipo `GiorniDellaSettimana` e assegnarle un valore:
>
>```java
>GiorniDellaSettimana oggi = GiorniDellaSettimana.LUNEDI;
>```
>
>Puoi anche confrontare i valori delle enum utilizzando gli operatori di confronto, come ==:
>
>```java
>if (oggi == GiorniDellaSettimana.LUNEDI) {
>    System.out.println("Oggi è lunedì!");
>}
>```

---
## Campi, Metodi, e Costruttori 

Le enum possono avere [[Java - Fields|campi]], [[Java - Methods|metodi]] e [[Java - Constructor|costruttori]]:
- **Campi:** che sono variabili di istanza che memorizzano informazioni relative a ogni costante dell'enum.
- **Metodi:** che vengono utilizzati per fornire funzionalità alle costanti dell'enum.
- **Costruttori:** che vengono utilizzati per inizializzare i campi di ogni costante dell'enum.

>[!warning] Costruttori Privati
>È importante notare che i costruttori di un enum devono essere `private`, il che significa che non possono essere chiamati da fuori dell'enum. Ciò garantisce che le costanti dell'enum siano create solo una volta e che non possano essere modificate dopo la creazione.

>[!note] Esempio
>```java
>public enum Animali {
>	CANE("Cane", "Canis lupus familiaris"),
>	GATTO("Gatto", "Felis catus"),
>	TOPO("Topo", "Mus musculus");
>
>	// Campi
>	private final String nomeComune;
>	private final String nomeScientifico;
>
>	// Costruttore
>	Animali(String nomeComune, String nomeScientifico) {
>		this.nomeComune = nomeComune;
>		this.nomeScientifico = nomeScientifico;
>	}
>
>	// Metodi
>	public String getNomeComune() {
>		 return nomeComune;
>	}
>
>	public String getNomeScientifico() {
>		return nomeScientifico;
>	}
>}
>```
>
>**Main:**
>```java
>Animali animale = Animali.CANE;
>System.out.println("Nome comune: " + animale.getNomeComune());
>System.out.println("Nome scientifico: " + animale.getNomeScientifico());
>```

#### Metodi Polimorfici

Quando si definiscono metodi polimorfici all'interno di un enum, ogni costante dell'enum può avere una propria implementazione del metodo, il che consente di definire comportamenti diversi per ogni costante.

>[!note] Esempio
>```java
>public enum Animali {
>    CANE {
>        @Override
>        public String suono() {
>            return "Woof!";
>        }
>    },
>    GATTO {
>        @Override
>        public String suono() {
>            return "Miao!";
>        }
>    },
>    TOPO {
>        @Override
>        public String suono() {
>            return "Squeak!";
>        }
>    };
>
>    public abstract String suono();
>}
>```

---
## Interfacce ed Enum

>[!info] Interfacce
>In Java, un'interfaccia è un tipo di astrazione che definisce un insieme di metodi che devono essere implementati dalle classi che implementano l'interfaccia. 
>
>>**Leggi:** [[Java - Interfaces]]

Le enum pos[](Java%20-%20Interfaces.md)tare interfacce, il che significa che devono fornire implementazioni per tutti i metodi definiti nell'interfaccia.

Per implementare un'interfaccia in un enum, si utilizza la parola chiave `implements` dopo la dichiarazione dell'enum, seguito dal nome dell'interfaccia. Successivamente, si forniscono le implementazioni dei metodi definiti nell'interfaccia all'interno della enum.

>[!note] Esempio
>```java
>public interface Suonabile {
>    String suono();
>}
>
>public enum Animali implements Suonabile {
>    CANE("Woof!"),
>    GATTO("Meow"),
>
>    private final String verso;
>
>    @Override
>    public String suono() {
>        return verso;
>    }
>}
>```
>
>In questo esempio, abbiamo definito un'interfaccia `Suonabile` che definisce un metodo `suona()` che restituisce una stringa che rappresenta il suono che fa un animale. La enum `Animali` implementa l'interfaccia `Suonabile`, il che significa che deve fornire un'implementazione del metodo `suona()`.

---
## Metodi predefiniti Enums

```java
enum Size { 
   SMALL, MEDIUM, LARGE, EXTRALARGE 
}
```

1. `ordinal()`: Restituisce la posizione di una costante enum. Ad esempio, `ordinal(SMALL)` restituisce `0`.
2. `compareTo()`: Confronta le costanti enum in base al loro valore ordinale. Ad esempio, `Size.SMALL.compareTo(Size.MEDIUM)` restituisce `ordinal(SMALL) - ordinal(MEDIUM)`.
3. `toString()`: Restituisce la rappresentazione stringa delle costanti enum. Ad esempio, `SMALL.toString()` restituisce `"SMALL"`.
4. `name()`: Restituisce il nome definito di una costante enum in forma di stringa. Il valore restituito dal metodo `name()` è finale. Ad esempio, `name(SMALL)` restituisce `"SMALL"`.
5. `valueOf()`: Prende una stringa e restituisce una costante enum che ha lo stesso nome della stringa. Ad esempio, `Size.valueOf("SMALL")` restituisce la costante `SMALL`.
6. `values()`: Restituisce un array di tipo enum che contiene tutte le costanti enum. Ad esempio, `Size[] enumArray = Size.values()`.

>[!warning]  Possibili Errori
>Non sono sicuro che questi esempi siano giusti al 100%, ma per ora non sono riuscito a trovare niente di meglio.

