---
created: 2024-05-21
type: Uni Note
class:
  - "[[Metodologie di Programmazione (class)]]"
academic year: 2023/2024
related: 
completed: false
updated: 2024-07-10T20:41
---
>[!abstract] Index
>1. [[#Introduzione]]
>2. [[#Classificazione]]
>3. [[#Catalogo]]

>[!abstract] Related
>- [[Metodologie di Programmazione (class)]]

---
## Introduzione

I **Design Patterns** sono soluzioni tipiche a problemi comuni nel design del software.

Un pattern non è un codice specifico, ma un concetto generale per risolvere uno specifico problema. Applicare un design patter significa seguire i dettagli del pattern (ovvero la descrizione dell soluzione al problema) ma implementando una soluzione che si adatti alla realtà specifiche del tuo programma.

>[!note] Struttura di un Patter
>
>Solitamente un design patter è descritto tenendo ini considerazione questi aspetti:
>- **Intenzione:** Breve descrizione sia del problema che della soluzione.
>- **Motivazione:**  Spiegazione dettagliata del problema e della soluzione resa possibile dal modello.
>- **Struttura** delle classi mostra ogni parte del modello e come sono correlate.
>- **Esempio:** Codice in uno dei linguaggi di programmazione più popolari per rende più facile da comprendere l'idea alla base del modello.

>[!warning]- Differenza tra design Pattern e Algoritmo
>I pattern vengono spesso confusi con gli algoritmi, perché entrambi descrivono soluzioni tipiche a problemi noti. 
>
>**Algoritmo:**
>- Un algoritmo definisce sempre un insieme chiaro di azioni che possono raggiungere un obiettivo.
>
>**Pattern:**
>- Un pattern è una descrizione più generale di una soluzione. Il codice dello stesso pattern applicato a due programmi diversi può essere diverso.
>
>Un'**analogia** per un algoritmo è una ricetta di cucina: entrambi hanno passaggi chiari per raggiungere un obiettivo. D'altra parte, un pattern è più simile a un modello: puoi vedere qual è il risultato e le sue caratteristiche, ma l'ordine esatto di implementazione dipende da te.

>[!warning]- Criticità dei Design Patterns
>**Soluzioni inefficienti:**
>- I pattern cercano di sistematizzare approcci che sono già ampiamente utilizzati. Questa unificazione è vista da molti come un dogma, e implementano i pattern "alla lettera", senza adattarli al contesto del loro progetto.
>
>**Utilizzo ingiustificato:**
>- `Se tutto ciò che hai è un martello, tutto sembra un chiodo`. 
>- Questo è il problema che affligge molti principianti che si sono appena familiarizzati con i pattern. Avendo imparato i pattern, cercano di applicarli ovunque, anche in situazioni in cui un codice più semplice andrebbe benissimo.

>**Source:** [Refactoring Guru](https://refactoring.guru/design-patterns)

---
## Classificazione 

I design patters possono differire in complessità, livello di dettaglio e scala di applicabilità.
- **Idioms (idiomi)** sono pattern semplici e a basso livello, e solitamente possono essere applicati ad un singolo linguaggio di programmazione.
- **Architectural patters (patter architetturali)** sono modelli più universali e di alto livello, che possono essere utilizzati in qualsiasi linguaggio e sono utilizzati per progettare l'intera struttura du un applicazione.

I modelli possono essere categorizzati anche in base al loro scopo:
- **Creational Patterns (modelli creazionali):** forniscono meccanismi di creazione degli oggetti che aumentano la flessibilità e il riutilizzo del codice.
- **Structural Patterns (modelli strutturali):**  spiegano come assemblare oggetti e classi in strutture più ampie, mantenendo flessibili e efficienti le strutture.
- **Behavioral Patterns (modelli comportamentali):** si occupano della comunicazione efficace e dell'assegnazione dei compiti tra gli oggetti.

>**Source:** [Refactoring Guru](https://refactoring.guru/design-patterns)

---
## Catalogo

>[!note] Creational Patterns
> - [[Singleton (Design Pattern)|Singleton]] 🟢
> - [[Builder (Design Pattern)|Builder]] 🟢

>[!note] Structural Patterns
>- [[Decorator (Design Pattern)|Decorator]] 🔴

>[!note] Behavioral Patterns
>- [[Strategy (Design Pattern)|Strategy]] 🟢
>- [[Observer (Design Pattern)|Observer]] 🔴
