---
type: MOC
created: 2023-06-05
class:
  - "[[Metodi matematici per l'informatica (class)]]"
updated: 2024-05-27T13:29
---
---
# Indice
- [[#Proposizione]]
- [[#Lettere proposizionali]]
- [[#Costanti]]
- [[#Formula ben formata (definizione)]]
- [[#Interpretazioni]]
- [[#Formula soddisfacibile ed falsificabile]]
- [[#Tautologie, contraddizioni, contingenze]]
 
- [[Connettivi logici]]
- [[Leggi Logiche]]

- [[Metodo dei Tableaux nella logica proposizionale]]

- [[Sistemi Assiomatici (Hilbert systems)]] <--

Extra: [[Notazione polacca]]

---
## Proposizione
Una **proposizione semplice** (o atomica) è un’affermazione che: 
-  non dipende da variabili
-  può essere vera o falsa
-  viene formalizzata da un simbolo enunciativo

*Esempi:* 
- Ogni triangolo si può inscrivere in un cerchio *vera* 
- Roma è in Francia *falsa*

Una **proposizione composta** può essere:
-  sempre vera
-  sempre falsa
-  vera o falsa in funzione dei componenti

---
## Lettere proposizionali
Chiamiamo *lettere proposizionali* i simboli con p, q, r, . . .  con i quali indichiamo le variabili Booleane, ossia variabili che possono assumere valore True o False 

---
## Costanti
Esistono altre 2 lettere proposizionali `t` e `f` che indicano rispettivamente le variabili Booleane T e F

**Oss:**
- p ∧ f è equivalente a f mentre p ∧ t è equivalente a p 
- p ∨ f è equivalente a p mentre p ∨ t è equivalente a t 
- f ∧ t è equivalente a f mentre f ∨ t è equivalente a t

---
## Formula ben formata (definizione)
- Una **formula** è una sequenza di variabili e connettivi
- Una **formula ben formata** rispetta queste regole:
	1. Ogni *variabile* è una formula
	2. Se *x* è una formula allora *¬x* è una formula
	3. Se *x* e *y* sono formule allora *x* **\*** *y* sono una formula ben formata
		-  dove **\*** è un [[Connettivi logici|connettivo logico]]
	4. Nient’altro è una formula ben formata
	
---
## Interpretazioni
*Definizione:* 
- 


**oss:** in una tabella di verità ogni riga rappresenta una diversa interpretazione

- Data una formula `P` ed una interpretazione `τ` di `P`,
- `P` o è T (vera) o è F (falsa) nell’interpretazione τ. 

*Esempio:*
La formula (p ∨ q) ∧ ¬r
- è F (falsa) nell’interpretazione (p, q, r) = ( T , F , T)
- è T nell’interpretazione (p, q, r) = ( T , F , F )

---
## Formula soddisfacibile ed falsificabile
**Formula soddisfacibile:** esiste almeno un'interpretazione che la verifica

**Formula in-soddisfacibile:** non esiste un'interpretazione la verifichi (*non so se è giusto*)

**Formula falsificabile:** esiste almeno un'interpretazione che la falsifica

---
## Tautologie, contraddizioni, contingenze
- *Tautologie*  o formule valide formule che sono T (vere) in ogni interpretazione 
- *Contraddizioni:* formule che sono F (false) in ogni interpretazione
- *Contingenze:* formule che sono T in alcune interpretazioni e F in altre

>[!warning] Oss:
>**Formula valida** = tautologia


---


**Definire il concetto di soddisfacibilità nella logica proposizionale:**

- Una formula è soddisfacibile se almeno un’interpretazione la verifica.

  

**Definire il concetto di soddisfacibilità nella logica predicativa:**

- Una formula predicativa si dice soddisfacibile quando esiste almeno un modello

  

**Definire il concetto di interpretazione nella logica proposizionale:**

- Data una formula, chiamiamo interpretazione della formula un’assegnazione di verità alle sue variabili 

  

**Definire il concetto di interpretazione nella logica predicativa:**

- Interpretare significa dare un significato ad ogni predicato e scegliere un dominio.

  

 **Definire il concetto di modello nella logica predicativa:**

- Un modello è un’interpretazione che verifica una formula.

  

  

  

Relazione di ordine totale
- Va Vb  (R(a,b) or R(b,a))  

Relazione simmetrica
- Va Vb (R(a,b) -> R(b,a))

Relazione anti-simmetrica
- Va Vb ((R(a,b) and R(b,a)) -> a = b)

Relazione riflessiva
- Va R(a,a)

Relazione anti-riflessiva
- Va notR(a,a)

Relazione transitiva:
- Va, Vb  Vc ( (R(a,b)  and  R(b,c)) ->  R(a,c))

Sotto insieme 
- VX 3Y Vy (y in Y —>  y in X)

Esiste insieme vuoto
- 3X Vx not(x in X)  
- 3X not3x (x in X) 

  

Per ogni coppia di insiemi esiste la loro intersezione.

- VX VY 3Z Vz( (z in Z) <—> (z in X and z in Y )