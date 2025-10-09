---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2025-10-09T14:45
updated: 2025-10-09T15:33
---
L'API definisce in dettaglio il "contratto" di interazione tra il CONSUMER (il client) e il PROVIDER (il servizio). Essa specifica:
- Le richieste possibili.
- I parametri delle richieste.
- ﻿﻿I valori di ritorno.
- ﻿﻿Qualsiasi formato di dato richiesto (es. JSON, XML, YAML).


>[!note] Benefici
>
>L'adozione di un'API porta vantaggi fondamentali nell'architettura software:
>
>- ﻿﻿**Interfaccia Esplicita:** Definisce chiaramente le aspettative e le modalità di interazione.
>- ﻿﻿**Contratto Infrangibile:** Stabilisce un insieme di regole che entrambe le parti devono rispettare.
>- ﻿﻿**Information Hiding (Nascondimento delle Informazioni):** La logica interna del Provider (come i dati vengono processati o archiviati) rimane nascosta al Consumer. Il client deve solo conoscere l'interfaccia.

>[!note] API - Locali e Remote

>[!note] API - Private e Pubbliche

## Documentazione e Specifica delle API

Per stabilire il contratto, l'API deve essere definita esplicitamente.
- ﻿﻿La definizione può avvenire attraverso documentazione (testo, esempi, manuali).
- ﻿﻿Oppure, attraverso un linguaggio di descrizione standardizzato.

Un linguaggio di descrizione formalizza il contratto, consentendo la generazione automatica di documentazione, codice client e validazione.

>[!note] OpenAPI Specification (OAS
>
>OAS (OpenAPI Specification) è il linguaggio di descrizione leader del settore per le API moderne basate su HTTP.
>- ﻿﻿È un formato di descrizione vendor-neutral (indipendente dal fornitore) per le API remote basate su HTTP.
>- ﻿﻿Rappresenta lo standard industriale per la descrizione delle API moderne.
>- ﻿﻿E ampiamente adottato dalla comunità di svillupo
>  
>I file OpenAPI sono tipicamente scritti in formato YAML, dato la sua legibilità
>
>>[!example] Esempio
>>```yaml
>>openapi: 3.0.0 info:
>>	title: An example OpenAPI document 
>>	description: |
>>		This API allows writing down marks on a Tic Tac Toe board and requesting the state of the board or of individual cells.
>>	version: 0.0.1
>>paths: {} # Gli endpoint dell'API verrebbero definiti qui
>>```
