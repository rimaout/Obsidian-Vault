---
type: Programming Note
programming language: "[[Java MOC]]"
related:
  - "[[Software Design Pattern]]"
  - "[[Metodologie di Programmazione (class)]]"
completed: true
created: 2024-07-09T12:13
updated: 2024-07-09T15:10
---
>[!abstract] Index
>1. [[#Introduzione]]
>2. [[#Implementazione in Java]]

>[!abstract] Related
>- [[Software Design Pattern]]
>- [[Metodologie di Programmazione (class)]]
>- [[Java MOC]]

---
## Introduzione

Il Builder Pattern è un **design pattern creazionale** che viene utilizzato per costruire oggetti complessi. In particolare oggetti con molti attributi e parametri opzionali.

>[!note] Problemi
>Il Builder Pattern risolve diversi problemi comuni che possono sorgere durante la creazione di oggetti complessi:
>1. **Elimina la complessità dei costruttori con molti parametri**
>2. **Permette la creazione di oggetti immutabili:** Gli oggetti creati utilizzando il Builder Pattern possono essere resi immutabili una volta costruiti, garantendo che non possano essere modificati dopo la creazione.
>3. **Fornisce un'interfaccia chiara e flessibile per la creazione di oggetti:** Il Builder Pattern fornisce un'interfaccia per impostare i vari attributi di un oggetto in modo flessibile, consentendo di costruire oggetti complessi passo dopo passo.
>4. **Gestisce la creazione di oggetti con parametri opzionali:** Consente di gestire facilmente la creazione di oggetti con attributi opzionali, consentendo di impostare solo gli attributi necessari.

>[!note] Soluzione
>Il pattern del Builder risolve questo problema introducendo un oggetto separato chiamato "Builder" che è responsabile della costruzione dell'oggetto complesso. Il Builder inizializza i parametri "fondamentali" e fornisce una serie di metodi per configurare i parametri opzionali dell'oggetto.

---
## Implementazione in Java

Certamente! Posso generalizzare l'implementazione del Builder Pattern utilizzando una classe generica anziché la classe specifica Computer. Ecco una spiegazione più generale dell'implementazione del Builder Pattern:

>[!note] Struttura
>1. **Classe Generica:**
>    - La classe generica rappresenta l'oggetto complesso che vogliamo costruire. Può avere attributi obbligatori e opzionali.
>    - La classe generica ha un costruttore privato che accetta un oggetto Builder come argomento. Questo costruttore viene utilizzato per creare un'istanza della classe generica con gli attributi impostati dal Builder.
>
>2. **Classe Builder Generica:**
>    - La classe Builder generica è una classe statica nidificata all'interno della classe generica.
>    - Contiene gli stessi attributi obbligatori e opzionali della classe generica.
>    - Il costruttore della classe Builder accetta gli attributi obbligatori come parametri.
>    - La classe Builder fornisce metodi per impostare gli attributi opzionali. Questi metodi restituiscono l'istanza corrente del Builder per consentire la concatenazione dei metodi.
>    - Infine, la classe Builder fornisce un metodo build() che restituisce un'istanza della classe generica con gli attributi impostati.
>
>3. **Utilizzo del Builder Pattern:**
>    - Nel metodo main della classe di test, viene creato un oggetto utilizzando il Builder generico.
>    - Viene utilizzato il pattern fluent interface per impostare gli attributi opzionali in una singola riga di codice.
>    - L'oggetto viene creato chiamando il metodo build() del Builder.

>[!warning]- Esempio (video youtube)
>
>>**Video Tutoria:** [https://www.youtube.com/watch?v=D5NK5qMM14g](https://www.youtube.com/watch?v=D5NK5qMM14g)
>
>```java
>public class Computer {
>	
>	//required parameters
>	private String HDD;
>	private String RAM;
>	
>	//optional parameters
>	private boolean isGraphicsCardEnabled;
>	private boolean isBluetoothEnabled;
>	
>
>	public String getHDD() {
>		return HDD;
>	}
>
>	public String getRAM() {
>		return RAM;
>	}
>
>	public boolean isGraphicsCardEnabled() {
>		return isGraphicsCardEnabled;
>	}
>
>	public boolean isBluetoothEnabled() {
>		return isBluetoothEnabled;
>	}
>	
>	private Computer(ComputerBuilder builder) {
>		this.HDD=builder.HDD;
>		this.RAM=builder.RAM;
>		this.isGraphicsCardEnabled=builder.isGraphicsCardEnabled;
>		this.isBluetoothEnabled=builder.isBluetoothEnabled;
>	}
>	
>	//Builder Class
>	public static class ComputerBuilder{
>
>		// required parameters
>		private String HDD;
>		private String RAM;
>
>		// optional parameters
>		private boolean isGraphicsCardEnabled;
>		private boolean isBluetoothEnabled;
>		
>		public ComputerBuilder(String hdd, String ram){
>			this.HDD=hdd;
>			this.RAM=ram;
>		}
>
>		public ComputerBuilder setGraphicsCardEnabled(boolean isGraphicsCardEnabled) {
>			this.isGraphicsCardEnabled = isGraphicsCardEnabled;
>			return this;
>		}
>
>		public ComputerBuilder setBluetoothEnabled(boolean isBluetoothEnabled) {
>			this.isBluetoothEnabled = isBluetoothEnabled;
>			return this;
>		}
>		
>		public Computer build(){
>			return new Computer(this);
>		}
>
>	}
>
>}
>```
>
>```java
>public class TestBuilderPattern {
>
>	public static void main(String[] args) {
>		//Using builder to get the object in a single line of code and 
>                //without any inconsistent state or arguments management issues		
>		Computer comp = new Computer.ComputerBuilder(
>				"500 GB", "2 GB").setBluetoothEnabled(true)
>				.setGraphicsCardEnabled(true).build();
>	}
>
>}
>```

>[!warning]- Esempio (esercizio esame)

----

>[!info] Sources
>- https://refactoring.guru/design-patterns/builder
>- https://www.digitalocean.com/community/tutorials/builder-design-pattern-in-java
>- https://www.youtube.com/watch?v=D5NK5qMM14g
