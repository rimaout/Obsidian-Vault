---
type: Uni Note
class:
  - "[[TPFI]]"
academic year: 2024/2025
related:
completed: false
created: 2026-06-11T10:52
updated: 2026-07-11T17:16
---
## Funzion(al)i di Ordine Superiore

Dire che una funzione è di *ordine superiore* (spesso chiamata *funzionale*) significa che essa può:
- Prendere una o più funzioni come **argomento**.
- Restituire una funzione come **risultato**.

>[!example] Esempi
>
>- `map`: applica una funzione a ogni elemento di una lista.
>- `filter`: seleziona elementi in base a un predicato (funzione booleana).
>- `foldr`: generalizza i pattern di ricorsione sulle liste.
>- `(.)`: l'operatore di [[Function Composition - Haskell|composizione funzionale]], che combina due funzioni in una.
>  
>>[!warning]- Implementazioni
>>
>>Queste sono delle implementazioni di funzionali "famosi":
>>
>>```haskell
>>map :: (a->b) -> [a] -> [b]
>>map _ [] = []
>>map f (x:xs) = f x : map f xs
>>
>>filter :: (a->Bool) -> [a] -> [a]
>>filter _ [] = []
>>filter p (x:xs)
>>  | p x == True  =  x : filter p xs
>>  | otherwise    =  filter p xs
>>
>>foldr :: (a -> b -> b) -> b -> [a] -> b
>>foldr _ e [] = e
>>foldr f e (x:xs) = f x (foldr f e xs)
>>```

## Currificazione (Currying)

La **currificazione** è la proprietà per cui una funzione che accetta più argomenti viene trasformata in una sequenza di funzioni che accettano un solo argomento alla volta. Si fonda su un isomorfismo matematico:

$$A\times B\to C \cong A\to (B\to C)$$

In Haskell, **tutte le funzioni sono currificate di default**. Questo significa che una funzione definita come `f :: a -> b -> c` è in realtà una funzione che prende un tipo `a` e restituisce una nuova funzione di tipo `b -> c`.

>[!note] Vatanggi
>**Applicazione Parziale:** Permette di passare solo alcuni degli argomenti a una funzione, ottenendo una funzione "specializzata" pronta a ricevere i parametri mancanti.

## Strumenti per la Manipolazione Funzionale

Haskell fornisce funzionali predefiniti per la gestione della currificazione e delle funzioni di ordine superiore:

- **`curry`**: converte una funzione che accetta una coppia in una versione currificata: `((a, b) -> c) -> a -> b -> c`.
- **`uncurry`**: l'operato opposto, trasforma una funzione currificata in una che accetta una tupla: `(a -> b -> c) -> (a, b) -> c`.
- **`flip`**: inverte l'ordine dei primi due parametri di una funzione: `(a -> b -> c) -> b -> a -> c`.

## Eta-Regola

L'$\eta \text{-regola}$ (eta-reduction) permette di omettere un parametro se esso compare identico alla fine di entrambi i lati di un'equazione.

```haskell
f x = g x
-- equivalente a:
f = g
```

