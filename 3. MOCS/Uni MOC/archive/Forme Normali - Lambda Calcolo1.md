---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2026-06-12T19:05
updated: 2026-06-12T20:04
---
Nel contesto della valutazione *lazy* (o call-by-name), le **forme normali** descrivono il "livello di completamento" nel calcolo di un'espressione. 

In parole semplici, indicano a che punto un interprete (come quello di Haskell) può decidere di fermarsi o se deve continuare a calcolare.

## Normal Form (NF - Forma Normale)

La *Normal Form* indica lo stato di valutazione **massimo e completo**. Un termine si trova in Normal Form quando **non contiene alcun redex** (ossia non contiene più espressioni che possono essere ulteriormente ridotte o calcolate).

Nel $\lambda$-calcolo esempi tipici sono:

$$
\begin{align*}
&I = \lambda x.x\\
&K = \lambda xy.x\\
&\text{due} = \lambda sz.s(s(x))\\
&S = \lambda xyz.xz (yz)
\end{align*}
$$

In molti casi Haskell non arriva a ridurre un termine fino alla forma normale. Funzioni come `print` richiedono di ridurre un'espressione fino alla Normal Form perché, per poter stampare interamente un risultato a schermo, devono calcolarlo in ogni sua minima parte.

## Head Normal Form (HNF - Forma Normale di Testa)

- È una nozione del $\lambda$-calcolo legata alle riduzioni esterne.
    
- Un termine chiuso è in HNF se ha la forma esterna stabile $\lambda x_1 x_2 \dots x_n . x_i N_1 N_2 \dots N_m$.
    
- In questo stato, i sotto-termini interni ($N_1, N_2, \dots$) **non sono necessariamente valutati** (possono contenere ancora dei redex). Tuttavia, la struttura più esterna (la "testa") è ormai definita e non può più essere ridotta come un'applicazione funzionale.
    

## Weak Head Normal Form (WHNF - Forma Normale Debole di Testa)

Questo è il concetto in assoluto **più importante per comprendere Haskell**! Essendo un linguaggio _lazy_, la regola aurea di Haskell è fare il minor sforzo possibile: **valuta le espressioni fermandosi alla Weak Head Normal Form**, a meno che non ci sia un motivo strettamente necessario per andare oltre.

Un'espressione in Haskell si trova in WHNF se soddisfa uno dei seguenti criteri:
- **È una funzione (un'astrazione $\lambda$)**: ad esempio `\x -> x + 5` o la forma $\lambda x.M$ del $\lambda$-calcolo. Il corpo interno della funzione può contenere calcoli non eseguiti, ma l'espressione esterna è già una funzione e quindi è un valore.
- **È un costruttore di dati applicato al livello più esterno**: questo vale per le liste (dove il costruttore è l'operatore di concatenazione `:`) o per i tipi definiti dall'utente (come `Just`, `Left`, ecc.), **indipendentemente dal fatto che gli argomenti interni siano stati valutati o meno**.

**Esempi di WHNF in Haskell:**

- `(3+2) : [1, 2]` $\rightarrow$ È in WHNF perché il costruttore `:` si trova in testa. Il fatto che la testa contenga un calcolo irrisolto (`3+2`) non importa ad Haskell.
    
- `undefined : undefined` $\rightarrow$ Sorprendentemente, anche questa è in WHNF! La struttura esterna della lista c'è (sappiamo che non è vuota), anche se provare a valutare la testa o la coda genererebbe un errore.
    
- `Just (4 + 4)` o `Just undefined` $\rightarrow$ Sono in WHNF perché il costruttore `Just` racchiude l'espressione al livello più esterno.
    

### Perché questa differenza è fondamentale? (Esempi pratici)

Il segreto dell'efficienza della valutazione lazy sta nel fatto che molte funzioni si accontentano della WHNF senza pretendere la Normal Form completa:

1. **Il comportamento di `null` o `head`**: La funzione `null` controlla se una lista è vuota. Se esegui `null [undefined]`, la lista viene valutata solo fino alla sua WHNF, che corrisponde a `undefined : []`. La funzione `null` osserva la WHNF, vede che c'è il costruttore `:` (quindi la lista ha almeno un elemento) e restituisce immediatamente `False`. Non va mai a guardare cosa c'è _dentro_, evitando così di far fallire il programma con un'eccezione. Lo stesso fa `head`, che estrae la testa senza valutarla.
    
2. **Il comportamento di `length` e `take`**: Se scrivi `length (take 2 [undefined, undefined, undefined])`, l'interprete risponde tranquillamente `2`. Questo accade perché `take 2` "srotola" la lista quel tanto che basta a mostrare i primi due costruttori `:` (le WHNF della struttura), e `length` si limita a contare quanti costruttori ci sono senza mai forzare la valutazione degli elementi interni (`undefined`), i quali rimangono intonsi e non calcolati.
    

In sintesi, la **Normal Form** è il calcolo totale (profondo) , mentre la **Weak Head Normal Form** è il calcolo superficiale, strutturale, che permette ad Haskell di manipolare strutture infinite o parziali senza calcolare dati inutili.