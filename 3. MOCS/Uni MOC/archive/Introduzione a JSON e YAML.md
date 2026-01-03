---
type: Uni Note
class:
  - "[[WASA (class)]]"
  - \
academic year: 2024/2025
related:
completed: true
created: 2025-10-09T14:14
updated: 2025-10-14T12:10
---
## JSON (JavaScript Object Notation)

È un formato di testo leggero basato su un sotto insieme di Javascript, utilizzato per lo scambio e archivio di dati.

Si basa su soltanto due "concetti", gli `object` glie `array` questi permettono di avere un testo:
- facile da leggere per gli **umani**
- facile da analizzare e generare per le **macchine**

>[!note] Oggetto
>
>Collezione non ordinata di coppie `nome` : `valore` racchiuse 
>
>- ***nome***: è stringa scritta tra `""`, deve essere unica all'interno dell'oggetto (a.k.a. "chiave" o "campo")
>- ﻿﻿***valore***: è numero, stringa, booleano, null, array, object
>
>```json
>{
>    "WASA": {
>        "name": "Web and Software Architecture",
>        "semester": 1
>    }
>}
>```

>[!note] Array
>
>Elenco ordinato di valori, separati da virgole, racchiuso tra parentesi quadre (`[]`).
>
>```json
>{
>	"wasaWeekDays": ["tuesday", "thursday"]
>}
>```

**Esempio:**

```json
{
	"anobject": {
		"aNumber": 42,
		"astring": "This is a string",
		"aBoolean": true,
		"nothing": null,
		"anArray": [
			1, 
			{"name": "value", "anotherName": 12 },
			"something else"
		]
	}
}
```

## YAML

**YAML (YAML Ain't Markup Language)** è un l﻿Linguaggio di serializzazione dei dati **pensato per gli umani**.
- ﻿﻿Per file di configurazione, per archiviare dati (.yaml), o per scambiare dati.
- ﻿﻿Formato di testo (basato sull'indentazione Python).

```yaml
anobject:
	aNumber: 42
	astring: This is a string 
	aBoolean: true
	nothing: null
	anArray:
		- ﻿﻿1
		- ﻿﻿anotherobject:  
			someName: some value 
			someOtherName: 1234
		- ﻿﻿something else
```

>[!warning] YAML superset di JSON
>
>- ﻿﻿I file JSON sono YAML validi
>- ﻿﻿{ } accettati per le mappe (oggetti)
>- ﻿﻿[] accettati per le liste (array)
>- ﻿﻿# Qualsiasi cosa dopo un simbolo cancelletto è un commento
>- ﻿﻿I documenti possono opzionalmente iniziare con - - - e finire con . . .
>- ﻿﻿Un file può contenere più documenti
>
>```yaml
>anotherArray: [1, 2, 3]
>anotherObject: { "city": "Rome", "country": "Italy" } astringWithColon: "COVID-19: procedure >di accesso"
>aNumericString: "0649911"
>aLongString: |
>	this string spans
>	more lines
>```
