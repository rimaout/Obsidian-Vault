---
created: 2024-02-26
type: Uni Note
class:
  - "[[Algoritmi 1 (class)]]"
academic year: 2023/2024
related: 
completed: true
updated: 2025-02-27T18:36
---
---
## Index
1. [[#Algoritmo]]
2. [[#Strutture Dati]]
3. [[#Efficienza]]
4. [[#RAM (Random Acces Machine)]]

---
## Algoritmo

>[!def] Definizione:
>Un algoritmo è una sequenza di comandi “**elementari**” ed “**univoci**” che
terminano in un tempo finito ed operano su strutture dati.
>
> Esistono due tipi di [[Algoritmi Iterativi]] e [[Algoritmi Ricorsivi]]

>[!warning] oss
>- **Elementari:** possono essere interpretati in un solo modo
>- **Univoci:** non possono essere scomposti in comando più semplici

---
## Strutture Dati

>[!def] Definizione
> Strumenti per memorizzare e organizzare i dati e semplificarne l’accesso e la modifica.

>[!warning] oss
>Non esiste una struttura dati che vada bene per ogni problema, quindi dobbiamo
conoscere proprietà, vantaggi e svantaggi delle principali strutture dati.

---
## Efficienza

>[!def] Definizione
> Quantificazione delle esigenze degli algoritmi in termini di tempo e di spazio, ossia tempo di esecuzione e quantità di memoria
richiesta.

>[!warning] oss
>Un aspetto fondamentale che va affrontato nello studio degli algoritmi è la
loro efficienza.
>
Questo perché:
>-  I calcolatori sono molto veloci, ma non infinitamente veloci;
>- La memoria è economica e abbondante, ma non è né gratuita né illimitata.
>
Nel corso illustreremo il concetto di **costo computazionale** degli algoritmi,
in termini di numero di operazioni elementari e quantità di spazio di memoria
necessari in funzione della dimensione dell’input.

---
## RAM (Random Acces Machine)

Per studiare l’efficienza di un algoritmo dobbiamo ANALIZZARLO, cioè prevedere le risorse che esso richiede per la sua esecuzione, senza che tale analisi sia influenzata da una specifica tecnologia che, inevitabilmente, col tempo diviene superata.
- Per fare questo, dobbiamo avere un modello astratto di calcolatore, che sia indipendente dalla tecnologia usata.
- In questo corso consideriamo un modello astratto di calcolo detto RANDOM ACCESS MACHINE (RAM).
- La RAM è quindi una macchina astratta, la cui validità e potenza concettuale risiede nel fatto che non diventa obsoleta con il progredire della tecnologia.

**Nel modello RAM:**
- esiste un singolo processore, che esegue le operazioni sequenzialmente.
- esistono delle operazioni elementari, l’esecuzione di ciascuna delle quali richiede per definizione un tempo costante. (Es.: operazioni aritmetiche, letture, scritture, salto condizionato, ecc.)

**Misure di costo:**
- Faremo l’ipotesi che ogni operazione aritmetica o di confronto viene eseguita in tempo costante, indipendentemente dalla dimensione degli operandi.
- Questo criterio è detto MISURA DI COSTO UNIFORME.
- Sebbene utile, questo è un modello di costo non sempre realistico perché i dati potrebbero non essere rappresentabili in una sola parola di memoria, e quindi anche le operazioni aritmetiche non richiederebbero, in realtà, tempo costante.