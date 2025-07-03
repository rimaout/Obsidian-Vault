---
type: Uni Note
class: "[[Basi di Dati 2 (class)]]"
academic year: 2024/2025
related: 
completed: true
created: 2025-06-18T16:08
updated: 2025-06-18T17:39
---
## Introduzione

Il diagramma UML degli use-case à semplice e poco elaborato, permette di avere una visione ad alto livello di:
- Quali sono gli **attori** che possono *interagire con il sistema*.
- A quali **macro-funzionalità** gli attori definiti possono accedere.

Il diagramma però non definisce il funzionamento delle singole operazioni, per questo è utilizzato il documento di specifica degli use-case.

![[Pasted image 20250618173909.png|900]]

## Struttura

Le operazioni di use-case seguono la seguente struttura:

```
nome_operazione(parametri) :
	
	pre condizioni
	...
	...
	...

	post condizioni
	...
	...
	...
```

>[!warning] Note
>
>Non si utilizza `this` perché il diagramma degli use-case non descrive le operazioni di classe ma a delle operazioni più generali.
>
>Non è presente un **tipo di ritorno**, dato che le operazioni di use case modificano/creano gli oggetti, ma non calcolano dei valori

