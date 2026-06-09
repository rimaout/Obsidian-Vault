---
type: Uni Note
class:
  - "[[TPFI]]"
academic year: 2024/2025
related:
completed: false
created: 2026-06-09T11:51
updated: 2026-06-09T16:16
---
## Basic Voting System

Abbiamo una lista `votes`, che raccoglie tutte le preferenze sotto forma dei nomi dei candidati. Vogliamo determinare il candidato ha avuto più preferenze

**Idea Funzionale:** 
1. *comporre trasformazioni* fino a ottenere una lista `results` contenente coppie nella forma `(np, c)`, dove `np` è il *numero di preferenze* e `c` è il *nome del candidato*.  
2. *ordinare* la lista per numero di preferenze.
3. si prende l’ultimo elemento e si estrae la seconda componente, cioè il nome del candidato vincente.

```haskell
votes = ["Rossi", "Bianchi", "Verdi", "Bianchi",  "Bianchi", "Rossi"]
results = [(2, "Rossi"),(3, "Bianchi"),(1, "Verdi")]

winner :: Ord a => [a] -> a
winner = snd . last . sort . results
```

Ora però dobbiamo trasformare `votes` in `results` , l'idea più semplice consiste nel:

1. generare la *lista dei candidati* `cdts`, rimuovendo i duplicati da `votes`
2. generare lista dei numeri delle preferenze associate ad ogni candidato (usiamo `filter` e `lenght`)
3. uniamo le due liste per ottenere `results` (possiamo usare `zip`)

```haskell
votes = ["Rossi", "Bianchi", "Verdi", "Bianchi",  "Bianchi", "Rossi"]

results :: Eq a => [a] -> [(Int, a)]
results xs =  zip  (map (\x -> count x xs) cdts) cdts
  where
    count x = length . filter (==x)
    cdts = rmvDups xs

	rmvDups :: Eq a => [a] -> [a]
	rmvDups [] = []
	rmvDups (x:xs) = x : (rmvDups (filter (/=x) xs))

winner :: Ord a => [a] -> a
winner = snd . last . sort . results

-- Esecuzione
winner votes  -- output: "Bianchi"
```

>[!note] Considerazioni
>
>Porta a un **rapid-prototyping**, pensando alle trasformazioni di una struttura dati nel suo complesso, che generano un flusso, che passa diverse funzioni per trasformare i dati nel risultato.
>
>In questo caso `rmvDups` può essere ottimizzato passando da `O(n^2)` a `O(n log n)` se, effettuiamo un `sorting` prima di rimuovere i duplicati. 

>[!note] Versione di Graham Hutton (list comprehension)
>
>```haskell
>results :: (Ord a) => [a] -> [(Int,a)]
>results vs = sort [(count v vs, v) | v <- rmvDups vs] 
>	where  count x = length . filter (==x)
>```

## Ballots Voting System

Consideriamo un sistema elettorale più complesso. La lista di voti è composta non più da singole preferenza, ma da  liste di preferenze in cui ciascuno mette in ordine i candidati.

Il vincitore si ottiene eliminando iterativamente quelli che  ricevono meno prime scelte, ad esempio:

```haskell
ballots :: [[String]] 
votes = [[“Rossi”, “Verdi”], [“Bianchi”],  [“Verdi”, “Rossi”, “Bianchi”], [“Bianchi”, “Verdi”, “Rossi”], [“Verdi”]] 

-- si elimina Rossi 
votes’ = [[“Verdi”], [“Bianchi”], [“Verdi”, “Bianchi”],  [“Bianchi”, “Verdi”], [“Verdi”]] 

-- si elimina Bianchi 
votes’’ = [[“Verdi”],[],[“Verdi”], [“Verdi”],[“Verdi”]]
```

Per ottenere questi risultati possiamo riutilizzare la funzione `results`, inserendola in una funzione `rank` che prende una lista di *ballots* (lista di lista di preferenze) e utilizza la funzione `results` soltanto sul primo elemento di ogni lista.

Ad ogni utilizzo di rank otterremo i risultati del ballottaggio, con i partecipanti ordinati dal perdente al vincente (di quel ballottaggio).

```haskell
rank :: Ord a => [[a]] -> [a] 
rank = map snd . results . map head
```

Ad ogni ballottaggio dobbiamo rimuovere il perdente (primo elemento di `rank`) da ogni occorrenza delle liste in `ballots`, per farlo possiamo usare questa funzione `elim`:

```haskell
elim :: Eq a => a -> [[a]] -> [[a]] 
elim x = map (filter (/=x))
```

Quindi otteniamo il vincitore rimovendo ad ogni ballottaggio il perdente fino a quando non rimane un solo candidato:

```haskell
winnerB :: Ord a => [[a]] -> a 
winnerB bs = let (c:cs) = rank (rmvEmpty bs) 
	in if cs == [] then c -- ho finito  else winnerB (elim c bs)
	   else winnerB (elim c bs)
	
	where rmvEmpty = filter (/=[])
```

