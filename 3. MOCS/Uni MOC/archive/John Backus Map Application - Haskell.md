---
type: Uni Note
class:
  - "[[TPFI]]"
academic year: 2024/2025
related:
completed: true
created: 2026-07-11T17:16
updated: 2026-07-12T13:46
---
## Introduzione

**John Backus** (progettista di Fortran & Algol) nel 1978 scrisse un celeberrimo articolo che rilanciò la programmazione funzionale ponendo l’accento sulle sue virtù composizionali.  Fece l’esempio del prodotto scalare.

>[!warning] Prodotto Scalare
>
>In matematica, il prodotto scalare è un'operazione algebrica che prende due vettori (o sequenze di numeri) della stessa lunghezza e restituisce **un singolo numero** (chiamato, appunto, "scalare").
>
>Si calcola semplicemente moltiplicando tra loro gli elementi corrispondenti dei due vettori e sommando poi tutti i risultati. Se abbiamo due vettori $\vec{a}$ e $\vec{b}$ composti da $n$ elementi, la formula è:
>
>$$\vec{a} \cdot \vec{b} = \sum_{i=1}^{n} a_i b_i = a_1b_1 + a_2b_2 + \dots + a_nb_n$$
>
>**Ad Esempio:** Se $\vec{a} = [1, 2, 3]$ e $\vec{b} = [4, 5, 6]$
>- Moltiplichiamo le coppie: $(1 \times 4)$, $(2 \times 5)$, $(3 \times 6)$ $\rightarrow$ $4, 10, 18$
>- Sommiamo i risultati: $4 + 10 + 18 = 32$
>- Il prodotto scalare è **32**.

## Prima Implementazione

```haskell
-- idea: costruiamo la lista di coppie 
-- mappiamo la funzione uncurry (*)  
-- sommiamo i prodotti ottenuti  
ps1 xs ys = sum (map (uncurry (*)) (zip xs ys)) 

-- vediamo che numero è 1011 in binario 
ps1 (reverse [1,0,1,1]) [2^x | x<-[0..]] -- out: 11
```

- Rispetto ai programmi iterativi non ci sono accumulatori e indici
- `[0..]` è la lista infinita di tutti i naturali. Haskell è _lazy_, e poiché la prima lista ha 4 elementi, `zip` prenderà solo le prime 4 potenze della seconda lista.

>[!note] Program Calculation
>
>```haskell
>ps1 [5, 4, 9] [10^x | x <-[0..]]
>	= sum(map (uncurry (*)) (zip [5, 4, 9] [10^x | x <-[0..]]))   -- def. ps1
>	= sum(map (uncurry (*)) (zip [5,4,9] [1,10, 100, ...])) -- zip srotola le liste
>	= sum(map (uncurry (*)) [(5,1),(4,10),(9,100)]) -- applichiamo zip
>	= sum [(5*1),(4*10),(9*100)]   -- map applica uncurry (*) a tutti le coppie
>	= (5*1) + sum [(4*10),(9*100)] -- facciamo un passo di sum
>	= ... -- si ripetono i passi di sum fino alla fine della lista
>	= 945
>```
>
>Vedi: [[Program Calculations - Haskell]]

## Seconda Implementazione (Applicazione Parziale)

Per capire a fondo i meccanismi dell’ideologia funzionale, scriviamo un’altra versione del prodotto scalare che non utilizza `uncurry` e `zip`. Sfrutteremo invece uno dei concetti fondamentali di Haskell: il [[Funzioni di Ordine Superiore, Currificazione e η-regola|currying]] (o applicazione parziale).

Per procedere, ci occorre una funzione d'ordine superiore che prenda una lista di funzioni e una lista di argomenti, e applichi ordinatamente ciascuna funzione al rispettivo argomento. La chiameremo `applyL` (sebbene in letteratura, venga talvolta chiamata `zApp`):

```haskell
applyL :: [a -> b] -> [a] -> [b]
applyL (f:fs) (x:xs) = f x : applyL fs xs 
applyL _ _ = []
```

Ora possiamo definire il nostro prodotto scalare. L'obiettivo è trasformare il calcolo in una catena di tre passaggi:
1. **Creare le funzioni:** Mappando l'operatore di moltiplicazione `(*)` sulla prima lista `xs`, otteniamo una lista di funzioni _parzialmente applicate_. Ad esempio, se `xs = [2, 3]`, `map (*) xs` genera la lista di funzioni `[(* 2), (* 3)]`.
2. **Applicare le funzioni:** Utilizziamo `applyL` per applicare questa lista di "funzioni moltiplicatrici" alla seconda lista `ys`. Questo genera la lista dei prodotti finali.
3. **Sommare:** Infine, collassiamo la lista risultante passandola a `sum`.

```haskell
ps2 xs ys = sum (applyL (map (*) xs) ys)
```

## Terza Implementazione (Astrazione Totale e Laziness)

Possiamo spingere la composizione funzionale ancora oltre, rimuovendo persino la funzione `map`. Sfruttando la valutazione pigra di Haskell, possiamo generare l'applicazione delle funzioni usando esclusivamente `applyL` e la funzione `repeat`.

```haskell
ps3 xs ys = sum (applyL (applyL (repeat (*)) xs) ys)
```

>[!note] Funzionamento
>
>l calcolo procede in questo modo:
>- `repeat (*)` genera una **lista infinita** di operatori di moltiplicazione: `[(*), (*), (*), ...]`.
>- Il primo `applyL` applica questa lista infinita di moltiplicatori al primo vettore `xs`. Essendo Haskell un linguaggio _lazy_, la valutazione si ferma non appena gli elementi di `xs` si esauriscono. Il risultato è la nostra consueta lista di funzioni parzialmente applicate (es. `[(1*), (2*), (3*)]`).
>- Il secondo `applyL` esterno applica queste funzioni al vettore `ys`, generando la lista dei prodotti.
>- Infine, `sum` calcola il totale.

