---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2026-06-07T15:38
updated: 2026-06-09T16:16
---

## Introduzione ai Funzionali di Ripiegamento

I funzionali della famiglia **`fold`** (ripiegamento) rappresentano uno degli schemi di programmazione più potenti in Haskell, poiché permettono di generalizzare il pattern di ricorsione sulle liste in un unico operatore di ordine superiore. 

L'idea fondamentale è che un `fold` agisce sostituendo sistematicamente i costruttori della lista: il costruttore di cons (`:`) viene sostituito da una funzione binaria generica `#`, mentre la lista vuota (`[]`) viene sostituita da un valore seme `v`.

## Le Versioni del Fold

>[!note] foldr (Fold Right)
>
>È il principio di ricorsione fondamentale per le liste finite e generalizza le computazioni in cui i risultati vengono "raccolti" e calcolati al rientro dalla ricorsione.
>
>- **Logica**: `foldr (#) v [x, y, z] = x # (y # (z # v))`.
>- **Tipo**: `(a -> b -> b) -> b -> [a] -> b`.
>- **Caratteristica**: Grazie alla valutazione lazy, `foldr` può "tirare fuori" qualcosa subito, rendendolo adatto anche a lavorare con strutture dati infinite se la funzione iniettata non è stretta nel secondo argomento.

>[!note] foldr1
>
>È una variante di `foldr` pensata per funzioni che non hanno un elemento neutro ovvio per la lista vuota (come `min` o `max`).
>
>- **Logica**: Non richiede un valore seme iniziale perché utilizza l'ultimo elemento della lista come base.
>- **Limite**: Genera un errore se applicata a una lista vuota.

>[!note] foldl (Fold Left)
>
>A differenza della versione _right_, `foldl` generalizza le ricorsioni in cui si "spingono in avanti" i valori (accumulatori) durante la discesa ricorsiva.
>
>- **Logica**: `foldl (#) v [x, y, z] = ((v # x) # y) # z`.
>- **Efficienza**: La computazione inizia solo quando finisce la ricorsione. In un contesto lazy, questo può portare a un elevato consumo di memoria (_space leak_) perché accumula espressioni non valutate fino alla fine della lista.

>[!note] foldl' (Strict Fold Left)
>
>È la versione ottimizzata di `foldl`, definita utilizzando il funzionale **`seq`** per forzare la valutazione immediata dell'accumulatore ad ogni passo.
>
>- **Vantaggio**: Riduce drasticamente il consumo di spazio, passando da una complessità $\Theta(n)$ a una costante $\Theta(1)$.


## Fusion Law per foldr

La **Fusion Law** è una proprietà teorica che permette di combinare una funzione con un `foldr` in un unico passaggio. Essa ha la forma: **`f . foldr g a = foldr h b`**.

Secondo il teorema, questa uguaglianza è valida se sono soddisfatte tre condizioni:

1. **`f`** è una funzione **stretta** (`f undefined = undefined`).
2. **`f a = b`**.
3. **`f (g x y) = h x (f y)`** per ogni `x, y`.

Questa legge funge da meccanismo di induzione generalizzata e viene usata per ottimizzare i programmi o dimostrarne la correttezza tramite ragionamento equazionale.

## Esempi Pratici

Molte funzioni standard sono istanze di questi schemi:

- **Operazioni aritmetiche e logiche**: `sum = foldr (+) 0`, `and = foldr (&&) True`, `length = foldr (\x -> (+1)) 0`.
- **Manipolazione liste**: `concat = foldr (++) []` e `filter p = foldr (\x xs -> if p x then x:xs else xs) []`.
- **Inversione di lista**: `reverse` implementata con `foldr` ha complessità quadratica $\Theta(n^2)$, mentre con `foldl (flip (:)) []` diventa lineare $\Theta(n)$.

##  Scan e Unfold: I Duali del Fold

>[!note] scanl e scanr
>
>Queste funzioni sono simili ai fold ma, invece di restituire solo il risultato finale, producono la **lista di tutti i risultati intermedi** calcolati durante il processo.
>
>- **`scanl`**: Applica la funzione a tutti i prefissi. Può essere definita come `map (foldl f e) . inits`
>- **`scanr`**: Applica la funzione a tutti i suffissi, partendo dalle code.
>- **Esempio MSS**: Il problema della sotto-sequenza di somma massima può essere risolto in tempo lineare con `mss = maximum . scanr (@) 0`.

>[!note] unfold (Co-ricorsione)
>
>Mentre il fold "consuma" una struttura per produrre un valore, **`unfold`** è il suo duale: "genera" una struttura (come una lista o uno stream) a partire da un valore seme.
>
>- **Definizione**: `unfold p f y` usa un predicato `p` per decidere quando fermarsi e una funzione `f` per generare la coppia (elemento corrente, seme successivo).
>- **Utilizzi**: Permette di definire in modo elegante funzionali come `iterate`, `map` e `zip` in termini di produzione di dati invece che di consumo.

