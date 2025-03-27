---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-03-22T13:04
updated: 2025-03-25T11:46
---
1. Requisiti **Docenti Universitari**:
	- 1.1.  Nome (Stringa)
	- 1.2. Cognome (Stringa)
	- 1.3. Luogo di Nascita (Città)
	- 1.4. Data di Nascita (Data)
	- 1.5. Matricola (Stringa di sei caratteri interi, identifica univocamente il docente) 
	- 1.6. Posizione (tra Ricercatore, Professore associato, Professore ordinario)

2. Requisiti **Progetti di Ricerca**:
	- 2.1. Nome (Stringa, identifica univocamente il progetto di ricerca)
	- 2.2. Acronimo (Stringa, identifica univocamente il progetto di ricerca)
	- 2.3. Data inizio (Data)
	- 2.4. Data fine (Data >= Data inizio)
	- 2.5. Docenti partecipanti (vedi req. 1) 
	- 2.6. Lista di WB di cui è composto il progetto (vedi req. 5)

3. Requisiti **Attività Docenti**: **#**
	- 3.1. Un impegno deve essere di una sola tra queste tre categorie:
		- 3.1.1. Assenza
		- 3.1.2. Impegni istituzionali
		- 3.1.3. Impegni progettuali
	- 3.2 Un impegno deve avere una di queste due tipologie di durata:
		- Durata breve misurata in ore
		- Durata lunga misurata in giorni
	- 3.3. Data (Data)
	- 3.4. Motivazione (Stringa)
	- 3.5. Una sola tipologia scelta tra un insieme che varia in base alla categoria di attività:
		 - 3.5.1. Se la categoria è Assenza (vedi req. 3.1.1.) allora la tipologia è scelta tra: (chiusura universitaria, malattia, gravidanza, etc.)
		 - 3.5.2. Se la categoria è Impegni istituzionali (vedi req. 3.1.3.) allora la tipologia è scelta tra: (didattica, ricerca, missione, consiglio di dipartimento, consiglio di area didattica, etc.)
		 - 3.5.3. Se la categoria è Impegni progettuali (vedi req. 3.1.3.) allora la tipologia è scelta tra: (Ricerca e Sviluppo, Dimostrazione, Management, etc.)
	- 3.6. il docente che effettua l’attività (vedi req. 1)

4. Requisiti **Città**:
	- 4.1. Nome (Stringa, insieme a Nazione identica univocamente città)
	- 4.2. Nazione (Stringa, insieme a Nome identica univocamente città)

5. Requisiti **Work Package (WP)**:
	- 5.1. Fa riferimento ad un progetto di ricerca (vedi req. 2)
	- 5.2. Nome (Stringa)
	- 5.3. Data inizio (Data)
	- 5.4. Data fine (Data, >= di Data inizio)
