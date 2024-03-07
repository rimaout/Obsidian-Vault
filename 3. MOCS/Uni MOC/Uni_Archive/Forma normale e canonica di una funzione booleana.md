---
Created: 2023-10-16
Type: Uni Note
Class:
  - "[[Progettazione Sistemi Digitali (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Tabelle di verità, Maxtermini e Mintermini]]"
  - "[[Algebra Booleana]]"
Completed: true
---
---
## Index
1. [[#Forma normale]]
	- [[#Come ottenere forma normale]]
2. [[#Forma canonica]]
	-  [[#Come ottenere forma canonica]]

---
## Forma normale 
- **Sop:** forma normale (*disgiuntiva*)
	- rete: and-to-or
- **Pos:** forma normale (*congiuntiva*)
	- rete: or-to-and

**oss:** forma normale != [[Circuito ed espressione minimale|forma minimale]]

#### Come ottenere forma normale
1. Applicare leggi di demorgan (fino ad ottenere la complementazione sulle singole variabili)
2. Proprietà distributiva
3. Eliminare termini ripetuti (usare idempotenza)

---
## Forma canonica
**Sop:** tutti i termini prodotto sono min-termini (*disgiuntiva*)
**Pos:** tutti i termini somma sono max-termini (*congiuntiva*)

#### Come ottenere forma canonica
**Forma normale --> Forma canonica:**

- Forma canonica SOP: 
	- Moltiplicare il termine prodotto in cui manca x per (x+!x)
		![[IMG_2594.jpeg|600]]
	
- Forma canonica POS:
	- sommare al termine somma in cui manca x il prodotto x!x
		![[IMG_2593.jpeg|600]]

**Tabella di verità --> Forma canonica:**
- Forma canonica ***SOP***: 
	- Calcolare la funzione trovando i mintermini:
	![[Tabelle di verità, Maxtermini e Mintermini#Min-termine (1)]]
- Forma canonica ***POS***:
	- Calcolare la funzione trovando i max-termini: ![[Tabelle di verità, Maxtermini e Mintermini#Max-termine (0)]]
	![[IMG_5ABE40527815-1.jpeg]]


---