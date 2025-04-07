---
type: Uni Note
class: "[[Basi di Dati 2 (class)]]"
academic year: 2024/2025
related: 
completed: false
created: 2025-04-07T14:19
updated: 2025-04-07T15:56
---
1. Requisiti **officine**:
	- 1.1. Nome (Stringa)
	- 1.2. Indirizzo (vedi. req. 6)
	- 1.3. Numero dipendenti (intero)
	- 1.4. Anni di servizio di ogni dipendente (Data iniziale e Finale)
	- 1.5. Direttore (vedi req. 2.5) (uno solo)

2. Requisiti **dipendenti**:
	- 2.1. Nome
	- 2.2. Codice Fiscale
	- 2.3. Indirizzo
	- 2.4. Numero di Telefono (tipo numero di telefono con apposita specifica)
	- 2.5. Un dipendente può anche essere un Direttore, in questo caso ha delle informazioni aggiuntive:
		- 2.5.1. Data di nascita (Data)

3. Requisiti **riparazioni**:
	- 3.1. Codice (Intero)
	- 3.2. Veicolo (vedi req. 4)
	- 3.2. Data accettazione (Data)
	- 3.3 Ora accettazione (Ora)
	- 3.3. Data riconsegna (Data)
	- 3.3 Ora riconsegna (Ora)

4. Requisiti **veicolo**:
	- 4.1. Modello (Stringa)
	- 4.2. Tipo (enumerazione di tipologie)
	- 4.3. Targa (Stringa con definizione particolare)
	- 4.4. Anno di immatricolazione (Anno)
	- 4.5. Proprietario (vedi req. 5)

5. Requisiti **proprietario**:
	- 5.1. Nome (Stringa)
	- 5.2. Codice Fiscale (Stringa com specifica)
	- 5.3. Telefono (Stringa con specifica)

6. Requisiti **indirizzo**:
	- via
	- civico
	- città
	- cap

I dati di interesse per il sistema sono quelli relativi alle officine della catena, i relativi dipendenti e direttori, e quelli relativi alle riparazioni dei veicoli:
- Di ogni **officina** della catena interessano il nome, l’indirizzo, il numero di dipendenti, i dipendenti con il relativo numero di anni di servizio ed il direttore.
- Dei **dipendenti** e dei direttori interessano il nome, il codice fiscale, l’indirizzo e il numero di telefono; inoltre dei direttori interessa anche la data di nascita.
- Per quanto **riguarda le riparazioni dei veicoli**, sono dati di interesse il codice, il veicolo (modello, tipo, targa, anno di immatricolazione e proprietario), la data ed ora di accettazione e quella di riconsegna (per le riparazioni terminate).

Infine, dei proprietari dei veicoli interessano nome, codice fiscale, indirizzo e telefono.
