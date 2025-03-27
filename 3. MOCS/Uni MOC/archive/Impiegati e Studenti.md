---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-03-22T16:00
updated: 2025-03-22T16:26
---
1. Requisiti **Persona**:
	- 1.1. Nome (Stringa)
	- 1.2. Cognome (Stringa)
	- 1.3. Codice fiscale (Stringa che identifica univocamente una persona)
	- 1.4. Data di nascita (Data)
	- 1.5. Le persone devono essere o Uomo o Donna (vedi rispettivamente req. 2 e 3)
	- 1.6. Le persone possono essere o Impiegati o Studenti (vedi rispettivamente req. 4 e 6)
	 
2. Requisiti **Uomo**:
	- 2.1. Posizione militare (Obbligo al servizio militare, Attivo, Congedato, Esente, Riservista)

3. Requisiti **Donna**:
	- 3.1. Numero di maternità (intero)

4. Requisiti **Impiegato**:
	- 4.1. Stipendio (reale >= 0)
	- 4.2 Un ruolo tra segretario, direttore o progettista
		- 4.2.1 I progettisti possono essere responsabili di diversi progetti (vedi req. 5), e ci interessa conoscere i progetti di cui il progettista è responsabile.

5. Requisiti **Progetti**:
	- 5.1. Nome (Stringa che identifica univocamente il progetto)

6. Requisiti **Studente**:
	- 6.1. Matricola (Stinga che identifica univocamente lo studente)
