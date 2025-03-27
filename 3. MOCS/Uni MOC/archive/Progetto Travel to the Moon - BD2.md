---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-03-12T16:20
updated: 2025-03-26T15:47
---
## Raffinamento

1. Requisiti **crociere**:
	- 1.1. Codice (stringa) 
	- 1.2. Data di inizio (data)
	- 1.3. Data di fine (data)
	- 1.4. Nave utilizzata (v. req. 2)
	- 1.5. Itinerario seguito (v. req. 4)
	- 1.6. una tipologia tra:
		- 1.6.1. luna di miele
			- 1.6.1.1. sottotipo tra:
				- 1.6.1.1.1 tradizionali: quelle che prevedono un numero di destinazioni romantiche (v. req. 3.4.1)
				- 1.6.1.1.2 alternative
				- : quelle che prevedono un numero di destinazioni romantiche (v. req. 3.4.1)
		- 1.6.2. per famiglie, di cui ci interessa:
			- 1.6.3 se adatte ai bambini (booleano)

2. Requisiti **navi**:
	- 2.1. Nome
	- 2.2. Grado di confort (un interno tra 3 e 5)
	- 2.3. Capienza (un intero > 0)

3. Requisiti **destinazioni**:
	- 3.1. Nome
	- 3.2. Continente
	- 3.3. Posti da vedere (v. req. 5)
	- 3.4. Tipo, uno tra:
		- 3.4.1. Romantica
		- 3.4.2. Divertente
	- 3.5. Se è esotica, ovvero se si trova in un continente diverso dall'Europa

4. Requisiti **Itinerari**:
	- 4.1. Nome
	- 4.2. Una sequenza ordinata di elementi, di cui interessa:
		- 4.2.1. Destinazione (v. req. 3)
		- 4.2.2. Arrivo, descritto da:
			- 4.2.2.1. Ora
			- 4.2.2.2. Numero d'ordine del giorno (rispetto alla data di inizio della crociera)
	- 4.3 ripartenza

5. Requisiti **posti da vedere**:
	- 5.1. Nome
	- 5.2. Orari di apertura (una mappa che associa ad ogni giorno della settimana una fascia oraria, in termini di coppia di orari)


## Specifica

Specifica della classe crociera:
- un'istanza di questa classe rappresenta una crociera

operazione di classe:
- fine(): Data
	- Pre-condizioni: nessuna
	- post-condizioni: 