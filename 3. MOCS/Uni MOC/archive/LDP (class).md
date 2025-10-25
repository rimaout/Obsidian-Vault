---
type: "[[Uni MOC]]"
academic year: 2024/2025
completed: false
created: 2025-09-30T12:25
updated: 2025-10-23T11:00
---
- [Dispenze Prof.]()
- [Dispenze Exiss.](https://raw.githubusercontent.com/Exyss/university-notes/main/Bachelor/Terzo%20Anno/Linguaggi%20di%20Programmazione.pdf)


- [[Algebre e strutture dati induttive]]

SML

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

## Numeri di Church in ML

Definiamo il numero due usando i numeri di Church

```lisp
val due = (fn x => fn y => x (x y));
```

Ora definiamo eval, una funziona che prende un numeoro di Church r ritorna l'intero associato ad esso:

```lisp
val eval = (fn z => (z (fn x => x+1) 0));
```

Testiamo due:

```lisp
eval due; --output: val it = 2 : int
```

Ora implementiamo:

```lisp
va
```