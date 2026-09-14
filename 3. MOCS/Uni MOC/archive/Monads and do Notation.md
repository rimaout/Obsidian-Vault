---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2026-07-14T16:16
updated: 2026-07-14T16:16
---
Here is a clear, formatted note you can copy and paste directly into your study materials.

## Haskell Study Notes: `do` Notation and The "One Monad" Rule

### 1. What is `do` Notation?

`do` notation is **syntactic sugar** for the bind operator (`>>=`). It allows you to write monadic code in a way that looks like sequential, imperative programming.

Under the hood, every `<-` arrow is translated by the compiler into a `>>=` operation.

Haskell

```
-- With do notation
addMaybe :: Maybe Int -> Maybe Int -> Maybe Int
addMaybe mx my = do
    x <- mx
    y <- my
    return (x + y)

-- What the compiler actually sees
addMaybe mx my = mx >>= (\x -> my >>= (\y -> return (x + y)))
```

### 2. The Golden Rule: One `do` Block = One Monad

You **cannot mix different monads** (like `Maybe` and `IO`) using `<-` inside the same `do` block.

> **Why?** Because `do` translates to `>>=`, and the type signature of `>>=` is:
> 
> `(>>=) :: Monad m => m a -> (a -> m b) -> m b`
> 
> Notice there is only one `m`. The monad on the left side of the bind **must perfectly match** the monad on the right side.

#### ❌ The Trap: Mixing Monads (Will not compile)

If a function's type signature says it returns `IO`, then every single statement in that `do` block using `<-` (or standing alone) must result in `IO`.

Haskell

```
-- ERROR: Trying to bind a Maybe inside an IO block
printValue :: IO ()
printValue = do
    x <- Just 5          -- Type error! 'Just 5' is Maybe, but this block is IO.
    putStrLn (show x)    
```

### 3. How to Work Around It

If you need to handle a different monad inside a `do` block, treat it like regular data instead of trying to bind it with `<-`.

**Solution A: Use `let` and Pattern Matching**

The `let` keyword binds pure values or data to variables without invoking `>>=`. Once bound, you can use a `case` expression to unpack it.

Haskell

```
-- CORRECT: Using 'let' and 'case' instead of '<-'
printValue :: IO ()
printValue = do
    let myValue = Just 5    -- 'let' doesn't care about the IO context!
    
    case myValue of
        Just x  -> putStrLn ("The value is: " ++ show x)
        Nothing -> putStrLn "No value found."
```

**Solution B: Monad Transformers (Advanced)**

When you genuinely need the features of two monads simultaneously (like `IO`'s side effects + `Maybe`'s failure handling), Haskell provides **Monad Transformers** (e.g., `MaybeT`). These allow you to stack monads together to create a single, combined context that _can_ be used with `<-` in a single `do` block.