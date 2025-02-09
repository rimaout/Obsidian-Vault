---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: false
created: 2025-02-08T22:04
updated: 2025-02-08T22:55
---
Le eccezioni sono un meccanismo utile per segnalare e gestire condizioni anomale ed errori che impediscono la normale esecuzione del programma.

Ci sono due tipologie di errori:

**Sincroni** si verificano dopo l'esecuzione di un'istruzione e possono essere gestiti tramite un eccezione, si dividono in:
- ***Errori non critici:*** Condizioni anomale (divisione 0)
- ***Critici*** Errori interni alla JVM (conversioni non consentita mancanza di memoria)

**Asincroni** avvengono per parallelamente all’esecuzione del programma e sono indipendenti dal flusso di controllo, non possono essere gestiti via software



Un'eccezione è una classe che eredita `Exception`, sono utilizzate per segnalare una condizione che impedisce la normale prosecuzione del programma e quindi interrompe l'esecuzione.

Possiamo definire le nostre eccezioni personalizzate che poi verranno generate dai nostri metodi, se un metodo genera un’eccezione deve dichiararlo nel nell'intestazione.

```java
class MiaEccezione extends Exception { ... }

class MiaClasse {
	private Utente amministratore;

	public void leggiInformazioni(Utente u) throws MiaEccezione {
		if(!amministratore.equals(u)) throw new MiaEccezione();
	}
}
```


## Tipologie d'errori / eventi