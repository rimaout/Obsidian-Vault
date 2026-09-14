---
type: Uni Note
class:
  - "[[TPFI]]"
academic year: 2024/2025
related:
completed: true
created: 2026-06-05T14:49
updated: 2026-07-08T16:11
---
## Introduzione

**Lists** are *homogeneous* (= same type) sequences of values, that can be processed sequentially. 

The simpler way to construct a list is by using the constructor `[]`, but this is just syntactic sugar for the  *infix operator*  **cons** (`:`). It it can be seen as a *head insert* and its name derives from *constructor*.

Foe example this writing `[1,2,3]` it's just syntactic sugar for `1:2:3:[]`.

## x:xs 

Tutte le liste hanno la forma `x:xs` dove: 
- `x` è la testa 
- `xs` rappresenta la coda (il resto della lista)

>[!note] Attenzione! 
>
>L’applicazione di funzione associa sempre più di tutto e quindi `f x:xs` viene inteso come `(f x):xs` e non come `f (x:xs)`.
## Lists Enumerations

Esistono **quattro modi** per dichiarare le enumerazioni di liste in Haskell:

>***Lista finita con passo predefinito:*** `[m..n]`
>
>Questa notazione genera una **lista finita** che parte da `m` e arriva fino a `n`, incrementando il valore di 1 ad ogni passo.
>
>**Esempio:** `[1..5]` produce `[1,2,3,4,5]`

>***Lista infinita con passo predefinito:*** `[m..]`
>
>Sfruttando la valutazione **lazy** di Haskell, questa notazione crea una **lista infinita** (uno _stream_) che parte da `m` e prosegue indefinitamente con incrementi di `1`.
>
>**Esempio:** `[1..]` è la lista di tutti i numeri naturali a partire da 1.

>***Lista finita con passo personalizzato:*** `[m,n..p]`
>
>Questa forma permette di definire il **passo della sequenza**. Il passo viene calcolato automaticamente come la differenza tra il secondo elemento (`n`) e il primo (`m`). La lista termina al raggiungimento di `p`.
>
>- **Logica:** Il passo è `n - m`. La sequenza sarà `[m, m+(n-m), m+2(n-m), ..., p]`.
>- **Esempio:** `[1, 3..11]` produce la lista dei numeri dispari fino a `11.

>***Lista infinita con passo personalizzato:*** `[m,n..]`
>
>Analogamente alla precedente, definisce il passo tramite i primi due elementi, ma genera una **lista infinita**.
>
>- **Esempio:** `[1, 3..]` genera la lista infinita di tutti i numeri dispari.

>[!warning] Note
>- **Non solo numeri:** Questa notazione non è limitata agli interi, ma può essere usata con qualsiasi tipo che appartenga alla classe `Enum`. Ad esempio, `['a'..'z']` genera correttamente la stringa contenente tutto l'alfabeto minuscolo.
>- **Limiti logici:** sebbene sia possibile definire passi costanti, la notazione non è in grado di inferire sequenze matematiche complesse. Ad esempio, scrivere `[1, 1, 2, 3, 5..]` **non** genererà la successione di Fibonacci.

## List Comprehension

Le **list comprehension** in Haskell sono un modo sintetico ed espressivo per manipolare le liste, ispirato direttamente alla notazione matematica della **set comprehension** basata sulla [[Logica del primo ordine (predicativa)]].

```haskell
[x^2 | x<-[1..5]] -- [1,4,9,16,25]
```

>[!note] Fondamenti Teorici
>
>In matematica, un insieme può essere definito come ${ x \in A \mid P(x) }$, ovvero l'insieme degli elementi `x` appartenenti ad `A` che soddisfano il predicato `P`. Haskell adotta una sintassi simile:
>
>- **Generatori**: La parte `x <- xs` indica da dove vengono estratti gli elementi.
>- **Filtri (Guards)**: I predicati inseriti dopo la virgola (es. `p x`) agiscono come filtri.
>- **Trasformazione**: Espressioni come `x^2` definiscono come trasformare l'elemento estratto.
>
>A livello teorico, le list comprehension non sono primitive, ma vengono **tradotte internamente in termini di `map` e `filter`**. Ad esempio:
>- `[f x | x <- xs]` equivale a `map f xs`.
>- `[x | x <- xs, p x]` equivale a `filter p xs`.

>[!note] Utilizzi
>
>Le slides forniscono diversi esempi di utilizzo, dai più semplici ai più complessi:
>
>- **Trasformazioni semplici**: `[x^2 | x <- [1..5]]` genera i quadrati dei numeri da 1 a 5.
>- **Pattern Matching**: È possibile decomporre strutture dati direttamente nel generatore. Ad esempio, per estrarre i primi elementi di una lista di coppie: `[x | (x, _) <- ps]`.
>- **Fattori di un numero**: Si possono usare le "guards" per calcolare i divisori: `factors n = [x | x <- [1..n], n 'mod' x == 0]`.
>
>Utilizzi avanzati
>
>- **Prodotto Cartesiano**: Usando più generatori, si ottengono tutte le combinazioni possibili.
>    - `[(x,y) | x <- [1,2,3], y <- [4,5]]` produce tutte le coppie.
>    - *Attenzione all'ordine*: L'ordine dei generatori influenza il risultato (il generatore più a destra cambia più velocemente, come un ciclo annidato).
>- **Flattening (concat)**: La funzione `concat` può essere definita come `[x | xs <- xss, x <- xs]`, dove si scorre prima la lista di liste e poi ogni singola lista interna.
>- **Funtori Applicativi**: La definizione standard dell'operatore applicativo `<*>` per le liste usa proprio una list comprehension: `gs <*> xs = [g x | g <- gs, x <- xs]`.

>[!danger] Limitazioni
>Sebbene Haskell sia **lazy** e permetta l'uso di generatori infiniti (es. `x <- [1..]`), bisogna prestare attenzione:
>
>- Se si usa una list comprehension con un filtro su una lista infinita e si cerca un elemento che non esiste, la computazione **non terminerà mai**.
>- **Esempio critico**: Cercare i fattori di un numero in una lista infinita di naturali senza un limite superiore porterà il programma a scansionare numeri all'infinito dopo aver trovato l'ultimo divisore. In questi casi è meglio usare funzioni come `takeWhile`.

## Funzioni su Liste

Most of the default functions in the `Prelude` are easy to recreate yourself, even the on that operate on lists.


**Taglio**: `take n` , `drop n` , `splitAt n` (tupla con take e drop).

```haskell
take 2 [1, 2, 3, 4]    -- risultato: [1, 2]
drop 2 [1, 2, 3, 4]    -- risultato: [3, 4]
splitAt 2 [1, 2, 3, 4] -- risultato: ([1, 2], [3, 4])
```

**Liste annidate/multiple:**
- `concat` (appiattisce liste di liste),
- `zip` (unisce liste in coppie, fermandosi alla più corta)

```haskell
concat [[1, 2], [3, 4]]    -- risultato: [1, 2, 3, 4]
zip [1, 2] ['a', 'b', 'c'] -- risultato: [(1, 'a'), (2, 'b')]
```

**Operazioni Logiche:**

```haskell
and [True, False]   -- risultato: False
or [True, False]    -- risultato: True
any (> 2) [1, 2, 3] -- risultato: True (almeno uno è > 2)
all (> 0) [1, 2, 3] -- risultato: True (tutti sono > 0)

myNull :: [a] -> Bool
myNull [] = True
myNull _ = False

myLast :: [a] -> a
myLast [x] = x
myLast (_:xs) = myLast xs

myInit :: [a] -> [a]
myInit [x] = []
myInit (x:xs) = x : myInit xs

mySum :: (Num a) => [a] -> a
mySum [] = 0
mySum (x:xs) = x + sum xs

myLenght :: [a] -> Int
myLenght [] = 0
myLenght (x:xs) = 1 + sum xs

myAnd :: [Bool] -> Bool
myAnd [] = True
myAnd (x:xs) = x && myAnd xs

myMinimum :: (Ord a) => [a] -> a
myMinimum [x] = x
myMinimum (x:xs) = min x (minimum xs)

myReverse :: [a] -> [a]
myReverse [] = []
myReverse (x:xs) = myReverse xs ++ [x]

myZip :: [a] -> [b] -> [(a,b)]
myZip [] _ = []
myZip _ [] = []
myZip (x:xs) (y:ys) = (x,y) : (zip xs ys)
```

