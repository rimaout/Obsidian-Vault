---
type: Uni Note
class:
  - "[[TPFI]]"
academic year: 2024/2025
related:
  - "[[Types, Polymorphism and Classes - Haskell]]"
completed: true
created: 2026-06-07T16:23
updated: 2026-06-08T15:10
---
>[!note] Related
>
>- [[Types, Polymorphism and Classes - Haskell]]

## Introduzione

In Haskell, le **classi** sono collezioni (o classificazioni) di tipi, analogamente a come i tipi sono collezioni di valori. Questa classificazione è di natura **algebrica**: una classe stabilisce un contratto (simile alle **interfacce Java**) che definisce quali operazioni un tipo deve supportare.

L'annotazione prima della freccia `=>` indica un **vincolo di classe**.

- **Esempio**: `mcd :: (Ord a, Num a) => a -> a -> a`.
- Qui `a` non è un tipo arbitrario, ma deve essere contemporaneamente un **sottotipo di** **Ord** (per usare `<` e `==`) e di **Num** (per usare `-`).
- Anche le costanti hanno tipi vincolati: `3 :: Num a => a` (può essere `Int` o `Float`, ma non `Char`).

## Classi Predefinite

Le classi possono contenere **codice predefinito** (implementazioni di default) per i loro metodi

>[!note] Eq (Equality Types)
>
>Definisce l'uguaglianza (`==`) e la disuguaglianza (`/=`).
>
>```haskell
>class Eq a where  
>    (==), (/=) :: a -> a -> Bool  
>    
>    -- Implementazione di default per /=
>    x /= y = not (x == y)
>```
>
>È sufficiente fornire il codice per `==`, poiché `/=` è derivato.

>[!note] Ord (Ordered Types)
>
>Sottoclasse di `Eq` per tipi i cui valori sono ordinabili. È sufficiente fornire il codice per `<`, poiché gli altri operatori sono interdefiniti.
>
>```haskell
>class Eq a => Ord a where  
>    (<),(<=),(>=),(>) :: a -> a -> Bool 
>    min, max :: a -> a -> a 
>    
>    min x y | x <= y = x | otherwise = y 
>    max x y | x <= y = y | otherwise = x 
>    x <= y = x < y || x == y 
>    x >= y = x > y || x == y 
>    x > y = y >= x && y /= x
>```

>[!note] Num, Show e Read
>
>- **Num**: Classe generica per tipi numerici che supportano `(+)`, `(-)`, `(*)`, `abs`, `signum`.
>- **Show**: Per convertire valori in `String` (`show :: a -> String`). Fondamentale per la stampa nell'interprete.
>- **Read**: Il duale di `Show`, converte una `String` in un valore (`read :: String -> a`).

## Definizione di Nuovi Tipi e Sinonimi

Haskell offre due modi principali per nominare i tipi:

>[!note] Sinonimi di Tipo (`type`)
>
>Crea alias per tipi esistenti. Non offre protezione sui dati (vige l'**equivalenza strutturale**) e non permette di definire nuove istanze.
>
>- `type Casella = (Int, Int)`
>- `type PairH a = (a, a)` (Sinonimo parametrico)

>[!note] Nuovi Tipi di Dato (`data`)
>
>Definisce un tipo completamente nuovo tramite **costruttori**. Solo questi tipi possono essere dichiarati istanze di una classe.
>
>- **Tipi Enumerati**: `data Giorni = Lun | Mar | Mer | Gio | Ven | Sab | Dom`.
>- **Tipi Parametrici**: `data Maybe a = Just a | Nothing`.
>- **Tipi Ricorsivi**: `data Nat = Zero | Succ Nat`.

## Istanze e Derivazione (`deriving`)

>[!note] Derivazione Automatica
>
>Per le classi standard (`Eq`, `Ord`, `Show`, `Read`, `Enum`), Haskell può generare automaticamente il codice tramite la clausola **deriving**.
>
>- L'uguaglianza derivata è **sintattica**.
>- L'ordinamento segue la **posizione dei costruttori** nella definizione.
>
>Esempio Completo: Il tipo `Giorni`
>
>```haskell
>data Giorni = Lun | Mar | Mer | Gio | Ven | Sab | Dom  
>    deriving (Eq, Ord, Show, Enum, Read)
>
>-- Esempi di utilizzo:
>lavorativi = [Lun .. Ven]         -- Grazie a Enum
>-- > [Lun, Mar, Mer, Gio, Ven]
>
>g = read "Lun" :: Giorni          -- Grazie a Read (richiede annotazione)
>-- > Lun
>
>domanda = Sab > Ven               -- Grazie a Ord (Sab viene dopo Ven)
>-- > True
>```

>[!note] Dichiarazione Manuale di un'Istanza
>
>Se vogliamo un comportamento personalizzato (es. una stampa diversa), usiamo `instance`:
>
>```haskell
>instance Show Giorni where
>    show Lun = "Lunedì"
>    show _   = "Altro giorno"
>```

## Costruttori di Tipo Avanzati

>[!note] Il tipo `Maybe`
>
>Usato per computazioni che possono fallire o produrre eccezioni.
>
>```haskell
>data Maybe a = Just a | Nothing
>
>safeDiv n 0 = Nothing
>safeDiv n m = Just (n `div` m)
>```

>[!note] Il tipo `Either`
>
>Rappresenta somme disgiunte, utile per valori che possono essere di due tipi diversi (es. un numero o una funzione).
>
>```haskell
>data Either a b = Left a | Right b
>
>-- Esempio: nodi di un albero di espressioni
>type Exp a = BinTree (Either (a -> a -> a) a)
>```
>
>![[Screenshot 2026-06-07 at 23.45.47.png|300]]
>
>Ecco la funzione di valutazione `expEval`.
>
>```haskell
>expEval :: Num a => Exp a -> a  
>expEval (R (Left f) l r) = f (expEval l) (expEval r) 
>expEval (F (Right v)) = v
>```
>
>E la valutazione dell’espressione in figura è `42`.

>[!note] Tipi Induttivi e Ricorsione
>
>Haskell eccelle nella gestione di strutture ricorsive come **Liste** e **Alberi**, definendo le funzioni per **pattern matching** sui costruttori.
>
>Esempio definizione strutture ricorsve:
>
>```haskell
>-- Lista Homemade
>data List a = Nil | Cons a (List a)
>
>-- Alberi binari F=Foglia, R=radice  
>data BTree a = Node a (BTree a) (BTree a) | Leaf a
>```
>
>Esempio definizione Funzioni:
>
>```haskell
>-- Lunghezza di una lista 
>length Nil = Zero 
>length (Cons _ l) = Succ (length l)
>
>-- append tra liste 
>append l Nil = l
>append Nil l = l 
>append (Cons x l) m = Cons x (append l m)
>
>-- visita inorder di un albero binario 
>flatten EMPTY = Nil
>flatten (Node x t1 t2) =
>	append (flatten t1) (Cons x (flatten t2))
>```


