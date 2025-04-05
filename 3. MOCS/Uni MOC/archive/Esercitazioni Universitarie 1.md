---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-03-31T22:59
updated: 2025-04-01T08:43
---
1. Requisiti **insegnamenti universitari**:
	-  1.1. Nome (Stringa, univoca)
	- 1.2. Crediti (Intero)
	- 1.3. Docenti (v. req. 3)
	- 1.4. Anno accademico (Anno)
	- 1.5. lista di esercitazioni (v. req. 2)

2. Requisiti **esercitazioni**:
	- 2.1. Data di erogazione (Data)
	- 2.2. Lista di Esercizi (v. req. 4) (*scelti tra quelli disponibili nel sistema*)

3. Requisiti **docenti**:
	- 3.1. Matricola (Stringa di 6 cifre numeriche, identifica univocamente il docente)
	- 3.2. Nome (Stringa)
	- 3.3. Cognome (Stringa)

4. Requisiti **esercizi**:
	- 4.1. Testo (Stringa)
	- 4.2. Soluzioni (v. req. 5) (uno o più, opzionale) (scelti tra quelli disponibili nel sistema)
	- 4.3. Gli esercizi possono far parte di un esercitazione (v. req. 2)
		- 4.3.1. se l'esercizio fa parte di una esercitazione allora ha una di queste due caratteristiche:
			- 4.3.1.1. Presentato (deve essere svolto in autonomia dagli studenti)
			- 4.3.1.2. Risolto (risolto in aula), a cui va allegato:
				- 4.3.1.2.1 Soluzioni mostrate agli alluni (v. req. 5) 

	1. Requisito **soluzione**:
	- 5.1. Esercizio da risolvere (v. req. 4)
	- 5.2. Testo (Stinga)