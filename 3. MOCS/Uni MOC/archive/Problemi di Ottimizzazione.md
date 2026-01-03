---
type: Uni Note
class: "[[Algoritmi 2 (class)]]"
academic year: 2024/2025
related: 
completed: true
created: 2025-04-07T11:06
updated: 2025-04-26T16:35
---
## Introduzione

Un problema di ottimizzazione è un tipo di problema in cui l'obiettivo è trovare la migliore soluzione possibile tra un insieme di soluzioni ammissibili.

>[!note] Soluzione Ammissibile
>
>Ogni soluzione ammissibile soddisfa tutte le condizioni imposte dal problema, ed ha un valore associato che può essere un **costo** o un **guadagno** (beneficio).
>

A seconda del tipo di problema, l'obiettivo può essere **minimizzare** il *costo* o **massimizzare** il *guadagno*. Per questo i problemi si dividono in problemi di *minimizzazione* e problemi di *massimizzazione*.

>[!example] Esempio
>
>Cercare in un grafo il percorso da `a` a `b` è un problema che ha come soluzioni ammissibili tutti i percorsi da `a` a `b`, ma se vogliamo il costo minimo fra questi scegliamo soltanto quello con costo minimo ovvero la soluzione ottima.

## Difficoltà

Per la maggior parte dei problemi\, trovare una **soluzione ottima** può avere una **complessità che cresce esponenzialmente** con la dimensione del problema.

Sebbene determinare l'ammissibilità di una soluzione può essere fatto in tempo polinomiale, trovare la soluzione ottima richiede, nella maggior parte dei casi, algoritmi molto più complessi e intensivi in termini di risorse computazionali. Per questo motivo si utilizzano algoritmi di approssimazione.

## Algoritmi di Approssimazione

Spesso non si hanno soluzioni efficienti per i problemi di ottimizzazione, ma soltanto esponenziali e quindi in questi casi ci si accontenta anche di una soluzione **ammissibile** che si avvicina ad una ottima.

Questa tipologia di algoritmi possono essere divisi in due categorie:

- **Algoritmi di Approssimazione** - Questi sono algoritmi per i quali è stato dimostrato che la soluzione fornita avrà *sempre* un certo grado di approssimazione rispetto alla soluzione ottima.
- **Euristiche** - Per questi algoritmi invece non si riesce a dimostrare un grado di approssimazione però osservando vari esperimenti si nota che generalmente si comportano bene. Di solito vengono visti come “l’ultima spiaggia” quando non si trovano altri algoritmi più efficienti.

Per ora approfondiamo gli algoritmi di approssimazione, iniziando con i problemi di minimizzazione

## Approssimazione dei Problemi di Minimizzazione

Iniziamo con problemi di minimizzazione dove ad ogni soluzione ammissibile è associato un costo e  quindi cerchiamo la soluzione ammissibile di costo minimo.

Si dice che `A` approssima il problema di minimizzazione entro un fattore di approssimazione `ρ` se per ogni istanza `I` del problema vale:

$$
\frac{A(I)}{OTT(I)} \leq \rho
$$

dove: 
- `OTT(I)` è il costo della soluzione ottimale applicata sull’istanza `I`.
- `A(I)` il costo della soluzione prodotta dall’algoritmo `A` per quell’istanza.

>[!danger] Costi
>
>- Se `A` approssima con fattore `1` allora è corretto perché trova sempre la soluzione ottima.
>- Se `A` approssima entro fattore `2` allora trova sempre una soluzione con al più il doppio del costo della ottima.
>
>Quindi più il rapporto è vicino a `1`, più l’algoritmo di approssimazione è buono.

## Approssimazione dei Problemi di Massimizzazione

Per i problemi di massimizzazione il ragionamento rimane invariato rispetto a quello appena visto per i problemi di minimizzazione, l'unica differenza è che per ogni soluzione ammissibile è preso in considerazione il rapporto inverso vale a dire:

$$
\frac{OTT(I)}{A(I)} \leq \rho
$$