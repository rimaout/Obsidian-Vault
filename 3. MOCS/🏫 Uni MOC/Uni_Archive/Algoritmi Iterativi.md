---
Created: 2024-03-22
Type: Uni Note
Class:
  - "[[Introduzione agli Algoritmi (class)]]"
Academic Year: 2023/2024
Related: 
Completed: true
---
---

>[!info] Index
>1. [[#Definizione]]
>2. [[#Istruzioni Elementari]]
>3. [[#Espressioni Condizionali]]
>4. [[#Istruzioni Iterative]]

Vedi anche: [[Esempi calcolo costo algoritmi iterativi ]]

---
## Definizione 

Un algoritmo iterativo è una tipologia di algoritmo che si basa sulla ripetizione di una o più azioni fino a quando non si verifica una condizione specifica. In altre parole, un algoritmo iterativo esegue un ciclo di passi ripetuti finché non raggiunge un determinato risultato o una specifica condizione di terminazione.

---
## Costo di un algoritmo iterativo

Il costo di un algoritmo iterativo è uguale alla **somma di tutti i costi delle parti che lo compongono**.

Può essere composta da:
- [[#Istruzioni Elementari]]
- [[#Espressioni Condizionali]]
- [[#Istruzioni Iterative]] (cicli)
- Funzioni (altri algoritmi) 

>[!danger] Attenzione
>Un algoritmo iterativo non può richiamare stesso ma soltanto altre funzioni (algoritmi)

---
## Istruzioni Elementari

Sono istruzione "di base" solitamente fornite dal linguaggio di programmazione che non possono essere semplificate in istruzioni più piccole

>[!note] Istruzioni elementari comuni
>- Operazioni aritmetiche
>- Lettura di un valore di una variabile
>- Valutazione di una condizione logica
>- Stampa di una variabile
>- Inizializzazione e assegnazione di una variabile
>- ecc

>[!warning] Costo Costante
>Solitamente le istruzione elementari hanno un costo costante che viene approssimato con $\Theta(1)$

---
## Espressioni Condizionali

Un’**istruzione condizionale** in algoritmica è un costrutto che permette di **verificare una condizione** e, a seconda del suo risultato, **eseguire diverse azioni**.

```python
if condizione1:
	istruzione1
	
else if condizione2:
	istruzione2

else:
	istruzione3
```

>[!warning] Costo 
>Il costo di delle espressioni condizionali è uguale alla **somma tra**:
>- Costo della verifica delle istruzione (solitamente costante)
>- Costo massimo tra i costi delle istruzzioni

---
## Istruzioni Iterative

Le istruzione iterative sono istruzioni che permettono di ripetere una determinata parte di codice finche una determinata condizione non è soddisfatta.

>[!note] Tipi comuni di istruzioni iterative
>- cilcli for
>- cicli while

>[!warning] Costo
>
>Le istruzioni iterative hanno un costo pari alla somma dei costi massimi di ciascuno iterazione (compreso il costo della verifica della condizione)
>
>Per calcolare il costo di un istruzioni iterativa è necessario stimare il numero di iterazioni.

---
