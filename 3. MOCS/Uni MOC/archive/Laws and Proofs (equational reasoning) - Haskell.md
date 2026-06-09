---
type: Uni Note
class:
  - "[[TPFI]]"
academic year: 2024/2025
related:
completed: false
created: 2026-06-08T15:11
updated: 2026-06-09T23:09
---
## Introduzione

Uno dei vantaggi principali della programmazione funzionale  che possiamo trattare i **programmi come espressioni matematiche** e *dimostrarne* la *correttezza* o l'*equivalenza* tramite leggi algebriche e induzione.

>[!note] l Principio: Program Calculation
>
>In Haskell, calcolare significa ridurre un'espressione. Poiché le variabili sono immutabili (legami tra nomi e valori, non indirizzi di memoria), un'uguaglianza come `f x = espressione` può essere usata in entrambe le direzioni:
>
>- **Sostituzione (da sinistra a destra)**: per eseguire il programma.
>- **Riconoscimento di pattern (da destra a sinistra)**: per semplificare o provare proprietà.

## Dimostrazione per Induzione Naturali

>[!note] Induzione Naturali ($m^{p+q} = m^{p} \cdot  m^{q}$)
>
>Dimostriamo nei naturali che `exp m (add p q) = mul (exp m p)(exp m q)` ovvero in matematichese:
>
>$$
>m^{p+q} = m^{p} \cdot  m^{q}
>$$
>
>Prima di tutto dobbiamo **definire le operazioni** e il tipo "naturale" (usiamo un tipo custom `Nat` perché evidenzia la struttura induttiva meglio degli `Int`)
>
>```haskell
>data Nat = Zero | Succ Nat -- Naturali Church
>
>add :: Nat -> Nat -> Nat
>add Zero n = n
>add (Succ m) n = Succ (add m n)
>
>mul :: Nat -> Nat -> Nat
>mul Zero n = Zero
>mul (Succ m) n = add n (mul m n)
>
>exp :: Nat -> Nat -> Nat
>exp x Zero = Succ Zero
>exp x (Succ n) = mul x (exp x n)
>```
>
>Ora dimostriamo `exp m (add p q) = mul (exp m p)(exp m q)`
>
>**Caso Base (`q = Zero`):**
>
>![[Screenshot 2026-06-08 at 16.09.37.png|700]]
>
>**Passo Induttivo (`q = Succ n`):**
>
>- *Ipotesi Induttiva:* Si assume che la proprietà (`exp m (add n q) = mul (exp m n)(exp m q)`) sia vera per `n` e si cerca di dimostrarla per il suo successore `Succ n`.
>
>![[Screenshot 2026-06-08 at 16.09.48 1.png|700]]
>
>Le parti evidenziate in verde sono esattamente i due termini della nostra **ipotesi induttiva** (la proprietà applicata a `n` invece che a `Succ n`). Poiché le assumiamo uguali, l'intera uguaglianza è dimostrata.

## Dimostrazione per Induzione Liste

Per provare che una proprietà `P(xs)` vale per tutte le liste (o strutture ricorsive), usiamo l'**induzione strutturale**:

1. **Caso Base**: Dimostri che `P([])` è vera.
2. **Passo Induttivo**: Assumi che `P(xs)` sia vera (**ipotesi induttiva**) e dimostri che allora è vera anche per `P(x:xs)`.

>[!note] Induzione su Liste Finite
>
>Dimostriamo questa uguaglianza pre **induzione strutturale** `xs ++ (ys ++ zs) = (xs ++ ys) ++ zs` tenendo in considerazione che l'operatore `++` è definito come:
>
>```haskell
>   []   ++ ys = ys           -- (1) 
>(x:xs) ++ ys = x:(xs ++ ys) -- (2)
>```
>
>**Caso Base (`xs = []`):**
>- *Parte Sinistra:* `[] ++ (ys ++ zs) = ys ++ zs` (per clausola (1) sul primo ++)
>- *Parte Destra:* `([] ++ ys) ++ zs = ys ++ zs` (per clausola (1) sul primo ++)
>- Ottenendo lo stesso risultato abbiamo dimostrato che il caso base è verificato
>  
>**Passo Induttivo (`x:xs`):**
>- Il nostro obbiettivo è partire da `((x:xs) ++ ys) ++ zs` (parte destra) e raggiungere `(x:xs) ++ (ys ++ zs)` (parte sinistra).
>- *Ipotesi Induttiva:* Si assume che la proprietà (`xs ++ (ys ++ zs) = (xs ++ ys) ++ zs`) sia vera per `xs` e si cerca di dimostrarla per `x:xs`.
>  
>```haskell
>((x:xs) ++ ys) ++ zs
 >	= 	(x:(xs ++ ys)) ++ zs 	-- per clausola (2) sul primo ++
 >	= 	x:((xs ++ ys) ++ zs) 	-- per clausola (2) sul secondo ++
 >	= 	x:(xs ++ (ys ++ zs)) 	-- per ipotesi induttiva
 >	= 	(x:xs) ++ (ys ++ zs) 	-- per clausola (2) inversa (FINE)
>```

>[!note] Lemma Reverse (distribuzione `reverse` su `++`)
>
>Dimostriamo questa uguaglianza `reverse (xs ++ ys) = reverse ys ++ reverse xs` tenendo in considerazione che `reverse` è definito come:
>
>```haskell
>reverse   []   = []                -- (1) 
>reverse (x:xs) = reverse xs ++ [x] -- (2)
>```
>
>**Caso Base (`xs = []`):**
>- *Parte Sinistra:* `reverse ([] ++ ys) = reverse ys` (per concatenazione con lista vuota=
>- *Parte Destra:* `reverse ys ++ reverse [] = reverse ys` (per clausola (1) su primo reverse e poi concatenazione con lista vuota)
>
>Ottenendo lo stesso risultato abbiamo dimostrato che il *caso base è verificato*.
>  
> **Passo Induttivo (`x:xs`):**
> - Il nostro obbiettivo è partire da `reverse ((x:xs) ++ ys)` (parte sinistra) e raggiungere  `reverse ys ++ reverse (x:xs)` (parte destra).
>- *Ipotesi Induttiva:* Si assume che la proprietà (`reverse (xs ++ ys) = reverse ys ++ reverse xs`) sia vera per `xs` e si cerca di dimostrarla per `x:xs`.
>
>```haskell
>reverse ((x:xs) ++ ys)
>	= reverse (z:(zs ++ ys))          -- per def. di ++
>	= reverse (zs ++ ys) ++ [x]       -- per clausola (2) di reverse
>	= reverse ys ++ reverse xs ++ [x] -- per ipotesi induttiva
>	= reverse ys ++ reverse (x:xs)    -- per clausola (2) inversa sul secondo reverse (FINE)
>```

>[!note] reverse è un’involuzione
>
>Dimostriamo che `reverse` è un involuzione ovvero che vale questa uguaglianza `reverse (reverse xs) = xs` tenendo in considerazione che `reverse` è definito come:
>
>```haskell
>reverse   []   = []                -- (1) 
>reverse (x:xs) = reverse xs ++ [x] -- (2)
>```
>
>**Caso Base (`xs = []`):**
>
>```haskell
>reverse (reverse [])
>	= 	reverse [] -- per clausola (1) su secondo reverse
>	= 	[]	       -- per clausola (1) su primo reverse
>```
>
>Dimostrato che `reverse (reverse []) = []` abbiamo verificato il caso base.
>
>**Passo Induttivo (`x:xs`):**
>
>- Il nostro obbiettivo è partire da `reverse (reverse (x:xs))` (parte sinistra) e raggiungere `(x:xs)` (parte destra).
>- *Ipotesi Induttiva:* Si assume che la proprietà (`reverse (reverse xs)`) sia vera per `xs` e si cerca di dimostrarla per `x:xs`.
>
>```haskell
>reverse (reverse (x:xs))
>	= reverse (reverse xs ++ [x])         -- per clausola (2) su secondo reverse
>	= reverse [x] ++ reverse (reverse xs) -- per lemma di "distibuzione reverse su ++"
>	= reverse [x] ++ xs                   -- per ipotesi induttiva
>	= reverse (x:[]) ++ xs                -- per definizione si lista
>	= reverse [] ++ [x] ++ xs             -- per clausola (2) di reverse
>	= [] ++ [x] ++ xs                     -- per clusola (1) di reverse
>	= [x] ++ xs                           
>	= (x:xs)                              -- FINE!
>```
>

^d68583
## Dimostrazioni di Equivalenza tra Composizioni

>[!note] map, head e undefined
>
>Dimostriamo che **`f . head xs = head . map f xs`** (se `f` è stretta)
>
>>***Nota:*** `f` è **stretta**, se `f udefined = undefined`
>
>---
>
>##### Caso Base (`[]`)
>
>>***Parte Sinistra***
>>
>>```haskell
>>f . head []
>>	= f (head []) -- per definizione di `.`
>>	= f undefined -- perche' head non è definita su lista vuota
>>	= undefined   -- perche' f è stretta
>>```
>
>>***Parte Destra***
>>
>>```haskell
>>head . map f []
>>	= head (map f []) -- per definizione di `.`
>>	= head []         -- per definizione di map
>>	= undefined       -- perche' head non è definita su lista vuota
>>```
>
>Ottenendo lo stesso risultato abbiamo dimostrato che il *caso base è verificato*.
>
>---
>
>##### Passo Induttivo (`x:xs`)
>
>- *Ipotesi Induttiva:* Si assume che la proprietà (`f . head xs = head . map f xs`) sia vera per `xs` e si cerca di dimostrarla per `(x:xs)`.
>
>
>>***Parte Sinistra***
>>
>>```haskell
>>f . head (x:xs)
>>	= f (head (x:xs)) -- per definizione di `.`
>>	= f x             -- per definizione di `head`
>>```
>
>>***Parte Destra***
>>
>>```haskell
>>head . map f (x:xs)
>>	= head (map f (x:xs))   -- per definizione di `.`
>>	= head (f x : map f xs) -- per definizione di `map` (logica lazy)
>>	= f x                   -- per definizione di `head`
>>```

## Dimostrate Map Funtore

