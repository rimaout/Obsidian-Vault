---
type: Uni Note
class:
  - "[[WASA (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-10-09T14:45
updated: 2025-10-14T12:34
---
Un **API (Application Programing Interface)** è la definizione delle interazioni consentite tra due parti si un software.

In particolare l'API definisce un "contratto" di interazione tra il ***CONSUMER*** (il client) e il ***PROVIDER*** (il servizio), essa specifica:
- Le *richieste* possibili
- I *parametri* delle richieste
- ﻿﻿I *valori di ritorno*
- ﻿﻿Qualsiasi *formato di dato* richiesto (es. [[Introduzione a JSON e YAML|JSON]], XML, [[Introduzione a JSON e YAML|YAML]]).

>[!check] Benefici
>
>L'adozione di un'API porta vantaggi fondamentali nell'architettura software:
>
>- ﻿﻿**Interfaccia Esplicita:** Definisce chiaramente le aspettative e le modalità di interazione.
>- ﻿﻿**Contratto Infrangibile:** Stabilisce un insieme di regole che entrambe le parti devono rispettare.
>- ﻿﻿**Information Hiding (Nascondimento delle Informazioni):** La logica interna del Provider (come i dati vengono processati o archiviati) rimane nascosta al Consumer. Il client deve solo conoscere l'interfaccia.

>[!note] API - Locali e Remote
>
>**API Locali:**  
>- API per i linguaggi di programmazione (es. la libreria standard di Python)
>- ﻿﻿API del sistema operativo
>- ﻿﻿API delle librerie software
>- ﻿﻿API hardware
>
>**﻿﻿API Remote (Web API):**
>- ﻿﻿Interfacce di programmazione basate su protocolli di rete (tipicamente HTTP), come le API [RESTful](https://it.wikipedia.org/wiki/Representational_state_transfer)

>[!note] API - Private e Pubbliche
>
>| Categoria | Descrizione | Restrizioni |
>| --- | --- | --- |
>| ***API Private*** | Utilizzo interno ad una azienda o sistema chiuso | L'accesso è limitato hai componenti interni |
>| ***API Publiche*** | Disponibili per l'uso de parte del publico | L'accesso può essere limitato solo ad alcuni utenti tramite **API Tokens** | 

>[!note] Interfaccia e Stabilità
>
>**Stabilità dell'Interfaccia**: I cambiamenti potrebbero rompere la compatibilità con i client esistenti.
>
>**﻿﻿Marcatori di Stato**:
>- *﻿﻿beta*: Indica che le parti potrebbero cambiare perché non sono ancora stabili.
>- *deprecated*: Indica che le parti verranno rimosse o non saranno più supportate in futuro.

## Documentazione e Specifica delle API

Per stabilire il contratto, l'API deve essere definita esplicitamente.
- ﻿﻿La definizione può avvenire attraverso **documentazione** (*testo*, *esempi*, *manuali*).
- ﻿﻿Oppure, attraverso un **linguaggio di descrizione standardizzato**.

Un linguaggio di descrizione formalizza il contratto, consentendo la generazione automatica di documentazione, codice client e validazione.

>[!note] OpenAPI Specification (OAS
>
>**OAS (OpenAPI Specification)** è il linguaggio di descrizione leader del settore per le API moderne basate su HTTP.
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
