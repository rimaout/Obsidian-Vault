---
created: 2024-03-05
type: Uni Note
class:
  - "[[Metodologie di Programmazione (class)]]"
academic year: 2023/2024
related: 
completed: false
updated: 2024-07-11T23:07
---
---
>[!info] Index
>1. [[#Basi]]
>2. [[#Classi]]
>3. [[#Struttura di una classe]]
>4. [[#Esempio classe]]
>5. [[#Modificatore della visibilità]]
>6. [[#Campi]]
>7. [[#Metodi]]
>8. [[#Costruttori]]
>9. [[#Variabili locali vs Campi]]
>10. [[#Incapsulamento]]
>11. [[#Interazione tra classi]]
>12. [[#UML (Unified Modeling Laguage)]]

---
## Basi

>[!note] Classe
>Una classe è un pezzo del codice sorgente di un programma che descrive un particolare tipo di oggetti
>- la classe fornice un prototipo astratto pre gli oggetti di un particolare tipo
>- Classi sono definite dal programmatore

>[!danger] ?
>Ne definisce la struttura in termini di:
>- Campi (stato) degli oggetti
>- Metodi (comportamenti) degli oggetti

>[!note] Oggetto 
>Un oggetto è un istanza di (un esemplare) di una classe

>[!warning] oss
>Un programma può creare e usare uno o più oggetti (istanze) della stessa classe


---
## Classi
Ogni classe è memorizzata in un file separato
- Il nome del file deve essere lo stesso della classe con estensione `.java`
- I nomi della classe iniziano sempre con la maiuscola, poi segue camel case

i membri di una classe sono `campi` e `metodi`

### Struttura di una classe
![[Pasted image 20240305092435.png|600]]


**Esempio classe**

![[Pasted image 20240305093325.png|800]]

>[!warning] oss
>- `void` indica che il metodo non ritorna niente come output 

[[Java Class and Objects]]

---
### Modificatore della visibilità
- `public`
- `private`

>[!warning] oss
>Metodi privati possono essere utilizzati da gli altri metodi della sua stessa classe ma non da metodi di classi esterne

[[Java Access Modifiers]]

---
### Campi 

>[!note] Definizione
>Un campo (detto anche variabile di istanza) costituisce la memoria privata di un oggetto
>- Ogni campo ha un tipo di dati (es. il valore del contatore è intero)
>- Ogni campo ha un nome fornito dal programmatore (es. value nella diapositiva precedente)

>[!tip] Dichiarazione
>`private [static] [final] tipo_di_dati nome`
>- `private`: tipicamente ad accesso privato
>- `static`: indica che il campo è condiviso da tutti gli oggetti 
>- `final`:indica che il campo è una cotante (il valore non può essere modificato una volta dichiarato) 
>
>*oss:* le parentesi quadre indicano l’opzionalità del parametro

[[Java Fields]]

---
### Metodi 
- Un metodo è tipicamente pubblico, ovvero visibile a tutti
- Il nome di un metodo per convenzione inizia con una lettera minuscola, mentre le parole seguenti iniziano con lettera maiuscola 


>[!tip] Dichiarazione
>`public tipo_di_dati nomeMetodo (tipo_di_dati nomeParametro1, ..., tipo_di_dati nomeParametro2)`

Esempio:
```java
public int getValue() {return value;}

public void reset(int newValue) {value = newValue;}
```

>[!example] Esempio:
**Implementazione di un metodo reset:**
>
>```java
>// versione 1
>public void reset() {value = 0} 
>
>// versione 2
>public void reset(int newValue) {value = newValue} 
>```

[[Java Methods]]

---
### Costruttori 
- I costruttori sono metodi "speciali" utilizzati per la creazione degli oggetti di una classe
- Possiedono sempre lo stesso nome della della classe (sono i costruttori hanno questa caratteristica)
- Inizializzano i campi dello stato iniziale di un oggetto
- Una classe può avere anche più costruttori che differiscono nel numero e nei tipi dei parametri ([[Java Overloading ]])

>[!warning] oss
>Non hanno valori in uscita ma non specificano void

Esempio più metodi costruttori nella stessa classe:
```java
public Counter(){
	value = 0;
}

public Counter(int initaliaValue){
	value = initialValue;
}
```

I **costruttori** vengono "chiamati" utilizzando `new NomeCostruttore()`
```java
static public void main(String[] args)
{
	Counter contatore1 = new Counter();
	Counter contatore2 = new Counter(42);
}

```

>[!danger] Non è obbligatorio definire un costruttore
>Infatti se non definiamo un costruttore utilizzerà un costruttore  di default che non ha nessun input e non ritorna nessun output

[[Java Constructor]]

---
## Variabili locali vs Campi 

I **campi** sono variabili dell’oggetto
- Sono visibili almeno all’interno di tutti gli oggetti della stessa classe
- Esistono per tutta la vita di un oggetto

Le **variabili locali** sono variabili definite all’interno di un metodo
-  Come parametri del metodo o all’interno del corpo del metodo
- Esistono dal momento in cui sono definite fino al termine dell’esecuzione della chiamata al metodo in questione

[[Java Fields#Campi vs. variabili locali]]

---
## Incapsulamento

>[!question] Perché utilizziamo le parole chiave public e private?
>- Per nascondere le informazioni (“information hiding”) all’utente

Il **processo che nasconde i dettagli realizzativi**, prende il nome di **incapsulamento**, che permette di utilizzare determinate classi senza conoscere il loro funzionamento attraverso un interfaccia publica

>[!note] Definition
>- Dettagli realizzativi: campi e implementazione
>- Interfaccia pubblica: metodi pubblici

Si semplifica e modularizza il lavoro di sviluppo assumendo un certo funzionamento a “scatola nera”
- Non è necessario sapere tutto, soprattutto molti inutili dettagli
- L’incapsulamento facilita il lavoro di gruppo e l’aggiornamento del codice (maintenance)
- Aiuta a rilevare errori: in presenza di moltissime classi, un certo errore si verifica solo in una determinata classe per cui ci si può concentrare su di essa

[[Java Incapsulamento]]

---
## Interazione tra classi
- Una classe interagisce con le altre principalmente (=quasi solo) attraverso i costruttori e i metodi pubblici

**Accesso a campi e metodi:**
- I campi e i metodi possono essere pubblici, privati (o protetti)
- I metodi di una classe possono chiamare i metodi pubblici e privati della stessa classe
- I metodi di una classe possono chiamare i metodi pubblici (ma non quelli privati) di altre classi

---
## UML (Unified Modeling Laguage)
- linguaggio universale che permette di disegnare (interpretare) diagrammi per la rappresentazione di programmi

[Libro link](https://personal.utdallas.edu/~chung/Fujitsu/UML_2.0/Rumbaugh--UML_2.0_Reference_CD.pdf)

**Object Oriented Analysis:**


**Reverse Engineering:**



---

 
