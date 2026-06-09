---
type: Uni Note
class:
  - "[[TPFI]]"
academic year: 2024/2025
related:
completed: true
created: 2026-06-05T15:27
updated: 2026-06-09T16:37
---
## Let

L'espressione `let` permette di definire **legami locali** (variabili o funzioni) validi esclusivamente all'interno di un'espressione specifica.

```haskell
let {legami} in {espressione}
```

L'espressione che segue la parola chiave **`in`** rappresenta il corpo principale del calcolo e il suo valore costituisce il **risultato finale (l'output)** dell'intera costruzione.

### Relazione con il Lambda Calcolo

Dal punto di vista semantico, il `let` è strettamente legato all'applicazione di funzioni nel lambda calcolo:
- L'espressione `let x = N in M` è logicamente equivalente all'applicazione `(\x -> M) N`.
- Tuttavia, esiste una differenza fondamentale nelle **regole di tipaggio** (nota come _let-polymorphism_): mentre nel lambda calcolo semplice il termine `(\x -> x x) (\y -> y)` non è tipabile, in Haskell l'espressione **`let x = \y -> y in x x` è correttamente tipabile**.
- **Perché?** Il costrutto `let` permette al sistema dei tipi di conoscere già la struttura del termine a cui $x$ è legato prima di valutarne l'auto-applicazione, limitando il polimorfismo alla struttura specifica del termine assegnato.

### Utilizzo Pratico: Decomposizione e Pattern Matching

Il `let` è uno strumento potente per "smontare" strutture dati complesse in modo conciso:
- **Decomposizione di tuple**: Permette di estrarre componenti da valori strutturati (es. `let (x, _) = z in x`).
- **Tupling**: È essenziale in tecniche come il _tupling_ per rendere efficienti algoritmi ricorsivi (es. la versione lineare di Fibonacci), dove viene usato per decomporre la coppia di risultati ottenuti dalla chiamata ricorsiva precedente.

```haskell
fibAux 0 = (0,0) -- il secondo valore non è importante 
fibAux 1 = (1,0) 
fibAux n =  
	let (f, fPrec) = fibAux (n-1) 
	in (f + fPrec, f)
	
fib n = fst (fibAux n)
```

### Efficienza: Lo Sharing

Uno degli utilizzi teorici e pratici più importanti del `let` riguarda l'ottimizzazione del codice in un sistema **lazy**:
- **Sharing degli argomenti**: Definire `sqr x = let y = x in y * y` assicura che $x$ venga valutato una sola volta anche se usato due volte nel prodotto (nota: l'input `x` potrebbe essere una funzione costosa da calcolare e non una costante)  .

### Logica "Bottom-Up"

A differenza della clausola `where` (che segue un approccio matematico top-down), il `let` promuove una logica **bottom-up**: prima si definiscono i componenti necessari (i "mattoni") e infine si assembla il risultato. Essendo un'**espressione standalone**, il `let` può essere utilizzato ovunque sia richiesto un valore, rendendolo estremamente versatile.

## Where

La clausola `where` serve a definire **legami locali** che qualificano i valori nella parte destra di una definizione.
- **Differenza cruciale**: A differenza di `let`, **`where` non è un'espressione**, ma una clausola sintattica.
- **Limite**: Non può essere utilizzata come espressione "standalone" (indipendente). Ad esempio, scrivere `x x where x = \x -> x` nell'interprete genera un errore di parsing perché `where` deve sempre essere attaccato a una definizione specifica.

### Teoria: Logica "Top-Down" e Ispirazione Matematica

Quindi `where` segue un approccio metodologico **top-down**.
- **Linguaggio Matematico**: Si ispira al modo in cui i matematici enunciano un teorema o una definizione, lasciandosi la libertà di specificare i dettagli in un secondo momento (es. _"Sia $f = h \circ g$, dove $h$ e $g$ sono..."_).
- **Leggibilità**: Questo permette di leggere immediatamente il risultato principale della funzione, rimandando la complessità implementativa alla fine della definizione. Per questo motivo, il "Vero Programmatore Haskell" (VPH) tende a preferirlo al `let`.

### Utilizzo Pratico: Decomposizione e Pattern Matching

Come il `let`, anche il `where` è uno strumento fondamentale per la **decomposizione** di strutture dati tramite pattern matching.

- **Esempio di estrazione**: `myFst z = x where (x, _) = z`.
- **Algoritmi complessi**: Viene usato per rendere il codice più pulito in algoritmi ricorsivi. Nella versione efficiente di Fibonacci, si definisce il risultato come una coppia e si specifica "dove" recuperare i valori calcolati: `fibAux' n = (f + fPrec, f) where (f, fPrec) = fibAux' (n-1)`.

```haskell
fibAux' 0 = (0,0) 
fibAux' 1 = (1,0) 
fibAux' n = (f+fPrec, f) where  
	(f, fPrec) = fibAux' (n-1) fib' n = fst (fibAux' n)
```

### Ambito di Visibilità (Scope)

I nomi definiti all'interno di una clausola `where` sono visibili esclusivamente all'interno della definizione che la clausola accompagna. Se una funzione ha più clausole (ad esempio con le "guardie"), il `where` è comune a tutte le guardie di quella specifica equazione.
