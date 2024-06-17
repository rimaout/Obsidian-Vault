---
type: Programming Note
programming language: "[[Java MOC]]"
related:
  - "[[Metodologie di Programmazione (class)]]"
completed: false
created: 2024-06-17T11:22
updated: 2024-06-17T11:40
---
>[!abstract] Index
>1. 

>[!abstract] Related
>- [[Java MOC]]
>- [[Metodologie di Programmazione (class)]]

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

Le enum possono avere anche valori aggiuntivi associati a ogni costante. Ad esempio:

```java
public enum Animali {
    CANE("Cane", "Canis lupus familiaris"),
    GATTO("Gatto", "Felis catus"),
    TOPO("Topo", "Mus musculus");

    private final String nomeComune;
    private final String nomeScientifico;

    Animali(String nomeComune, String nomeScientifico) {
        this.nomeComune = nomeComune;
        this.nomeScientifico = nomeScientifico;
    }
```

---

Le enum possono avere anche metodi e costruttori, se necessario. Tuttavia, è importante notare che i costruttori delle enum devono essere privati, in modo che non possano essere istanziate esternamente alla enum stessa.

Ecco un esempio di enum con un metodo:

```java
public enum GiorniDellaSettimana {     
	LUNEDI,     
	MARTEDI,     
	MERCOLEDI,     
	GIOVEDI,     
	VENERDI,     
	SABATO,     
	DOMENICA;     
	
	public boolean isFineSettimana() {         
		return this == SABATO || this == DOMENICA;     } 
}
```

In questo esempio, la enum `GiorniDellaSettimana` ha un metodo `isFineSettimana()` che restituisce `true` se il giorno della settimana è sabato o domenica, e `false` altrimenti.

Spero che questa lezione ti sia stata utile per capire come utilizzare le enum in Java! Se hai domande o dubbi, non esitare a chiedere.