---
type: "[[Uni MOC]]"
academic year: 2024/2025
completed: false
created: 2025-09-30T12:25
updated: 2025-10-27T18:20
---
- [Dispenze Prof.]()
- [Dispenze Exiss.](https://raw.githubusercontent.com/Exyss/university-notes/main/Bachelor/Terzo%20Anno/Linguaggi%20di%20Programmazione.pdf)

>[!note] Nozioni Preliminari
>
>...
>
>- [[Sintassi astratta dei linguaggi]] 🟢

>[!note] Paradigma Funzionale
>
>- [[Linguaggio Exp]]
>- [[Linguaggio Fun]]



## Lezione prima del 17 ott

```lua
let val x = 5 in x+1 end; --output: val it = 6 : int

(fn x => x+1) 9; --output: val it = 10 : int
```

ML è statico o dinamico? Testiamo runnando:
```lua
let val x = 7 in (let val y = x in (let val x = 9 in y end) end) end;

--output: val it = 7 : int
```

L'output è `7` e in questo caso solo un programma statico sarebbe `7`, quindi viene da pendare che ML è statico ma in realtà potrebbe essere eager e dinamico e dare comunque `7`

```lua
let val x = 7 in (let val y = (fn z => x) in (let val x = 9 in (y 3) end) end) end;

--output: val it = 7 : int
```

L'output è `7` quindi possiamo essere sicuri che ML è statico.

### Numeri di Church in ML

Definiamo il numero due usando i numeri di Church

```lisp
val due = (fn x => fn y => x (x y));
```

>[!example] Altri esempi
>
>```lisp
>val zero = fn x => fn y => y;
>```

Ora definiamo eval, una funziona che prende un numero di Church e ritorna l'intero associato ad esso:

```lisp
val eval = (fn z => (z (fn x => x+1) 0));
```

Testiamo due:

```lisp
eval due; --output: val it = 2 : int
```

>***oss:*** se a `due` che concatena due funzioni di arità uno (di fatto è come avere una funzione di arità due) quindi possiamo passargli due input ad esempio possiamo eseguire:
>
>```lisp
>due (fn x => x) 7; --output: 7
>```
>
>Infatti due avrà:
>- `x = (fn x => x)` (funzione di identità)
>- `y = 7`
> 
>Quindi l'output (`x (x y)`)  ovvero viene applicata due volte la funzione di indennità su 7

Ora implementiamo:

```lisp
val succ = fn w => (fn x => fn y => x (w x y));
```

Ho fatto w doppio + 1 volte xy

test:

```
eval (succ due): --output: val it = 3 : int
```

Ora implementiamo plus:

```lisp
val plus = fn u => fn v => (u (fn z => (plus z v)) zero);
```

Ora implementiamo times (prodotto):

```
val times = fn u => fn v => (u (fn z => (plus z v)) zero);
```

## Lezione 27 ott

