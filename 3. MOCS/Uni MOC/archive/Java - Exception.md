---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: false
created: 2025-02-08T22:04
updated: 2025-02-11T19:44
---

Le eccezioni sono classi che ereditano `Exception`, sono utilizzate per segnalare una condizione anomale che impediscono la normale prosecuzione del programma.

>[!note] Tipi di Errori
>
>Ci sono due tipologie di errori:
>**Sincroni** si verificano dopo l'esecuzione di un'istruzione e possono essere gestiti tramite un eccezione, si dividono in:
>- ***Errori non critici:*** Condizioni anomale del nostro codice (divisione 0)
>- ***Critici*** o irrecuperabili: Errori interni alla JVM (conversioni non consentita mancanza di memoria)
>
>**Asincroni** avvengono parallelamente all’esecuzione del programma e sono indipendenti dal flusso di controllo, non possono essere gestiti via software (completamenti nel trasferimento I/O)

## Gestione delle Eccezioni

**Politica del Catch or Declare:** indica che un metodo che può avere degli errori deve decidere se gestire l'eccezione utilizzando il blocco `try-catch` oppure se ignorarla utilizzando `throws`.

**Throws:** Se si decide di ignorare l'eccezione il metodo deve indicare il tipo di eccezione che può sollevare attraverso `throws`. Se tutti i metodi all’interno dell’albero delle chiamate dell’esecuzione decidono di ignorare l’eccezione, l’esecuzione viene interrotta, stampando la [[#^c29e66|stack trace]].


**Try-Catch:** Le eccezioni possono essere gestite attraverso il blocco `try-catch`  dove:
- nel blocco `try` vengono inserite le istruzioni che potrebbero ritornare un eccezione che vogliamo catturare
- nel intestazione del blocco `catch` definiamo il tipo di eccezione da gestire, all'interno del blocco si specifica l'azione da attuare a seguito dell’eccezione sollevata.

È possibile definire più blocchi `catch` per tipi di exception diverse me è importante dichiarali nel ordine giusto ovvero dalla catch più specifico al meno specifico. Infatti la JVM utilizza il primo catch compatible anche se non è il più specifico.

Dopo il costrutto `try-catch` è possibile inserire un blocco `finaly` che contiene del codice che verrà sempre eseguito dopo il blocco `try`, ad esempio la chiusura di un file.

>[!note] Stack Trace
>
>La stack trace è il messaggio a schermo che descrive l'errore, contenendo:
>- ***thread*** sul quale è stata sollevata l'eccezione
>- ***nome*** dell'eccezione
>- la successione in ordine inverso inverso delle invocazione dei metodi coinvolti.
>- ***file sorgente*** e il ***numero di riga*** di ogni invocazione

^c29e66

## Gerarchia delle Classi di Errore

![[Pasted image 20250210182429.png|600]]

Come radice della gerarchia abbiamo la classe `Throwable` che estende direttamente la classe `Object`. 

Come dirette sottoclassi di `Throwable` troviamo la classe `Error` e la classe `Exception`:

Le **Exception** possono essere divide in due categorie
- ***RuntimeException:*** ovvero eccezioni interne JVM legate ad errori nella logica del programma (es. `nullPointerException`)
- ***Eccezioni regolari:*** errori che le applicazioni dovrebbero anticipare e dalle quali poter riprendersi (es. `IOException`)

Gli **Error** riguardano condizioni di eccezione irrecuperabili, sono rari e non dovrebbero essere considerati dalle applicazioni

>[!note] checked e unchecked
>
>Eccezioni di tipo **checked**:
>- È sempre necessario attenersi al paradigma catch-or-declare
>- Sono eccezioni comuni, ovvero quelle che estendono ***Exception*** (ma non RuntimeException)
>- Esempi: `ParseException`, `ClassNotFoundException`, `FileNotFoundException`
>
>Eccezioni di tipo **unchecked**:
>- Non si è obbligati a dichiarare le eccezioni sollevate o a catturarle in un blocco try-catch (ma è possibile farlo)
>- Sono eccezioni che estendono ***Error*** o ***RuntimeException***
>- Esempi: `IndexOutOfBoundsException`, `ClassCastException`, `NullPointerException`, `ArithmeticException`, `OutOfMemoryError`

## Eccezioni Personalizzate

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
