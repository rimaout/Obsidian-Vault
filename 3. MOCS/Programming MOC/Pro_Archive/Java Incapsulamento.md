---
created: 2024-03-08
type: Programming Note
programming language: "[[Java MOC]]"
related:
  - "[[Java OOP]]"
completed: true
updated: 2024-06-18T11:44
---
>[!abstract] Index
>1. [[#Come funziona l'incapsulamento]]
>2. [[#Vantaggi dell'incapsulamento]]
>3. [[#Esempi]]

>[!abstract] Related
>- [[Java MOC]]
>- [[Object Oriented Programming (OOP)]]
>- [[Metodologie di Programmazione (class)]]

>[!danger] TLDR
>L'incapsulamento è un principio fondamentale della programmazione orientata agli oggetti ([[Object Oriented Programming (OOP)|OOP]]), che consente di creare classi con dati e comportamenti ben definiti e protetti, favorendo la modularità, la riusabilità e la manutenibilità del codice.

---
## Come funziona l'incapsulamento

L'idea alla base dell'incapsulamento è quella di nascondere i dettagli di implementazione di un oggetto, rendendo accessibili solo le informazioni necessarie all'esterno. Questo viene ottenuto attraverso l'utilizzo di modificatori di accesso, come `private`, `protected` e `public`, che consentono di controllare il livello di visibilità degli elementi all'interno della classe.

>[!note] Funzionamento
>**1. Incapsulamento dei dati:** 
>- Gli attributi di una classe vengono dichiarati come `private`, in modo che possano essere accessibili solo all'interno della classe stessa. Questo impedisce agli oggetti esterni di accedere direttamente ai dati dell'oggetto, evitando così manipolazioni indesiderate. 
>
>**2. Metodi di accesso (getter e setter):** 
>- Per consentire l'accesso ai dati incapsulati, vengono definiti dei metodi pubblici, chiamati getter e setter. I **getter** permettono di leggere il valore di un attributo, mentre i **setter** permettono di modificarlo. Questi metodi agiscono come interfaccia tra l'oggetto e il mondo esterno, garantendo il controllo sull'accesso e la modifica dei dati.
>
>**3. Incapsulamento del comportamento:** 
>- I metodi di una classe vengono dichiarati come `private`, `protected` o `public` a seconda del livello di visibilità desiderato. I metodi `private` sono accessibili solo all'interno della classe, mentre i metodi `public` possono essere chiamati da qualsiasi parte del codice. I metodi `protected` sono accessibili all'interno della classe e nelle sue sottoclassi. 

>[!warning] Access Modifiers 
>`private`, `protected` e `public` sono parole chiave in Java che consentono di controllare il livello di visibilità e accessibilità degli elementi (classi, attributi e metodi) e sono chiamati [[Java Access Modifiers|Access Modifiers]].

---
## Vantaggi dell'incapsulamento

>[!info] Vantaggi
>**1. Occultamento dell'implementazione:**
>- I dettagli di implementazione di un oggetto vengono nascosti, rendendo il codice più modulare e facile da manutenere.
>
>**2. Protezione dei dati:**
>- I dati dell'oggetto sono protetti da modifiche accidentali o non autorizzate, garantendo l'integrità dei dati.
>
>**3. Riusabilità del codice:**
>- L'incapsulamento facilita il riutilizzo del codice, in quanto gli oggetti possono essere utilizzati senza conoscere i dettagli di implementazione.
>
>**4. Flessibilità e estendibilità:**
>- È più semplice apportare modifiche all'implementazione di un oggetto senza influenzare il codice che lo utilizza.
>

---
## Esempio

Supponiamo di voler creare una classe `Persona` che rappresenta una persona. Vogliamo incapsulare i dati della persona, come il nome e l'età, in modo che possano essere accessibili e modificati in modo controllato.

```java
public class Persona {     

	// Attributi privati     
	private String nome;     
	private int eta;     
	
	// Costruttore     
	public Persona(String nome, int eta) {         
		this.nome = nome;         
		this.eta = eta;     
	}     
	
	// Metodi getter e setter     
	public String getNome() {         
		return this.nome;     
	}     
	
	public void setNome(String nome) {         
		this.nome = nome;     
	}     
	
	public int getEta() {         
		return this.eta;     
	}     
	
	public void setEta(int eta) {         
		if (eta >= 0) {this.eta = eta;} 
		else {System.out.println("L'età non può essere negativa.");}     
	}     
	
	// Metodo per stampare i dati della persona     
	public void stampaInfo() {         
		System.out.println("Nome: " + this.nome);         
		System.out.println("Età: " + this.eta);     
	} 
}
```

>[!note] Funzionamento
>**1. Incapsulamento dei dati:** 
>- Gli attributi `nome` e `eta` sono dichiarati come `private`, quindi sono accessibili solo all'interno della classe `Persona`.   
>
>**2. Metodi di accesso (getter e setter):** 
>- Sono stati definiti i metodi `getNome()`, `setNome()`, `getEta()` e `setEta()` per permettere l'accesso e la modifica dei dati incapsulati. Questi metodi agiscono come interfaccia tra l'oggetto `Persona` e il codice esterno.
>
>**3. Incapsulamento del comportamento:** 
>- Il metodo `stampaInfo()` è dichiarato come `public`, quindi può essere chiamato da qualsiasi parte del codice per stampare le informazioni sulla persona.

>**oss:** In questo esempio, l'incapsulamento garantisce che i dati della persona siano protetti e possano essere modificati solo attraverso i metodi `setter` appropriati. Inoltre, il metodo `stampaInfo()` fornisce un'interfaccia pubblica per accedere alle informazioni sulla persona.

