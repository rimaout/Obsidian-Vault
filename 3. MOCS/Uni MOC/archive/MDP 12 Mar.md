---
created: 2024-03-12
type: Uni Note
class:
  - "[[Metodologie di Programmazione (class)]]"
academic year: 2023/2024
related: 
completed: false
updated: 2024-05-27T13:29
---
---

>[!info] Index
>1. 

---
## Rappresentazione della memoria 
**Stack**
**Heap**
**Metaspace**

---
## Processo che fa la java virtual machine quando carica una classe
1. Analizzare campi statici:
	- Se presenti alloca i campi statici all’interno del meta space, i campi statici vengono inizianti con valori di default se nessun valore è dato.
2. Analizzare il metodo main
	- Viene creato un "frame" all’interno dello stack per il main
	- dentro il frame main viene creato un vettore di stringe args che punta a un oggetto dentro la heap
	- Eseguo le le operazioni all'interno dell' main
3. Quando viene chiamati un metodo quest'ultimo viene inizializzato nello stack
	- e vengono eseguite le operazioni al suo interno 
4. Quando chiamiamo un costruttore il nuovo oggetto viene allocato nella heap.
5. Quando viene chiamato un for, e quest’ultimo dichiara un contatore viene inizializzato com variabile locale all'interno del metodo di cui fa parte il for
6. Le variabili non statiche vengono inizializzate con valore `null` 

---
## Metodi statici
- i metodi statici sono metodi di classe
- Non hanno accesso ai campi di istanza
- Ma hanno accesso ai campi di classe

in altre parole hanno accesso soltanto alle loro variabili locali e hai campi statici della classe

---
## User input 
[[Java Input]]
- Si utilizza la classe java.util.Scanner
- Costruita passando al costruttore lo stream di input (`System.in` di tipo `java.io.Input.Stream)
- Blocca il programma in attesa di un input da tastiera

aggiungi esempio:
```java
// Crea uno scanner oer ottenere l'input
java.util.Scanner input = new java.util.Scanner(System.in)
```

---
## Package

>[!warning] oss
>L'unico package incluso di default in java è `java.lang`
>- Questo package non deve essere specificato

- Le classi vengono inserite (categorizzate) in collezioni dette package
- Ogni package racchiude classi con funzionalità correlate
- Quando si utilizza una classe è necessario specificarne il package (come per Scanner, che appartiene al package java.util)

**Importare una classe:**
- Utilizzata per non dichiarare il package ogni volta che si vuole utilizzare una determinata classe

```java
import java.util.Scanner;

// posso scrivere
Scanner input = new Scanner(System.in);

// invece di
java.util.Scanner input = new java.util.Scanner(System.in)
```

**Importare l'intero Package:**
- L’intero package:

```java
import java.util. \*;
```


>[!warning] \* non è ricorsivo
>Quindi i sub package contenuti dal main package non sono inportati

---
## Creazione di un nuovo package
- I package sono rappresentati fisicamente da cartelle (String.class si trova sotto java/lang/)
- Una classe può essere inserita in un determinato package semplicemente specificandolo all’inizio del file (parola chiave package)
- posizionando il file nella corretta sottocartella

---
## If else


---
## Switch case


**Switch case compatti**


**yield** 

---

---
## while, do while, for


---
