---
type: Uni Note
class:
  - "[[TPFI]]"
academic year: 2024/2025
related:
completed: false
created: 2026-06-05T10:09
updated: 2026-06-08T11:24
---
## Types

In Haskell it is used the notation:

$$
f :: X \to Y
$$

meaning that `f` is a function whose domain (= argument) is of type `X`, while the codomain (= result) is of type `Y`, similar to the usual mathematical notation.

>[!warning] Check the type
>
>If you are using the Haskell interpreter (`ghci`) you can check the type of a object using `:type`, for example:
>
>```haskell
>:type 5    -- 5 :: Num a => a
>:type 12.3 -- 12.3 :: Fractional a => a
>:type 4+8  -- 4+8 :: Num a => a
>:type sin  -- sin :: Floating a => a -> a
>```

## Type Constructors

Besides Integer, Float , Char and other predefined types, in Haskell there are type constructors.

**Lists** are the main data type, they are *homogeneous* (= same type) sequences of values, that can be processed sequentially. For example: `[3, 7, 11] :: [Integer]` and `[[], [3]] :: [[Integer]]`.

**Strings** are simply list of characters. Haskell offers a bit of syntactic sugar: `“tpfi”` stands for `[‘t’,’p’,‘f’,‘i’]::[Char]`

**Tuples** are n-uple of values, that can be *dis-homogeneous*. For example:  `(”pippo”, 5) :: ([Char], Integer)` and `(3, ’c’, (11, 3.14)) :: (Integer, Char, (Integer, Float))`

>***Note:*** It's important to note that **absence of mutable arrays**.
>***Note:*** see [[Lists - Haskell]]

## Polymorphism

Most function are defined on **universal qualifiers**, this means that can be used on all data types, for example the `++` operator can be used on all types of lists.

```haskell
[1,2,3] ++ [4,5]       -- [1,2,3,4,5] 
"I love " ++ "haskell" -- “I love haskell”
```

This is possible because `++` type is `(++) :: [a] -> [a] -> [a]`.

>***Attention:*** the type of (++) impose one constraint: the types of the two list arguments and that of the result, can be arbitrary, but the three lists must have the *same type*.

### Undefined

In Haskell it is pre-defined an `undefined constant`:

```haskell
Prelude> undefined
*** Exception: Prelude.undefined
```

More interestingly, the type of undefined:  

```haskell
undefined :: a
```

>[!warning] Nota
>
>- **Significato letterale**: Indica che "per ogni tipo possibile α, questo valore ha tipo α" ($\forall a.a$)
>- **Polimorfismo estremo**: È il tipo più generale possibile; ogni tipo specifico in Haskell (come `Int` o `Char`) è considerato un'**istanza** di questo schema.
>- **Inconsistenza logica**: È definito "inconsistente" perché nessun valore reale può appartenere a tutti i tipi contemporaneamente e fornire informazioni utili.
>- **Funzione pratica**: Proprio per la sua natura indefinita, funge da **rappresentazione canonica** per computazioni che falliscono (eccezioni) o che non terminano mai.

>[!note] Homemade Undefined
>
>Un modo per definere `undefined` "a mano" è: 
>
>```haskell
>myUndefined = myUndefined
>:type myUndefined -- myUndefined :: a
>```

## Classes

Classes are used to restrict the polymorphism of a function, for example, the sum operator (`+`) is still polymorphic, it restricted to the numeric types. To do this is used the class `Num`:

```haskell
(+) :: (Num a) => a -> a -> a
```

See: [[Classes and Subtyping - Haskell]]