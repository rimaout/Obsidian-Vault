---
type: Uni Note
class:
  - "[[TPFI]]"
academic year: 2024/2025
related:
completed: false
created: 2026-06-06T16:16
updated: 2026-06-06T16:22
---
In Haskell i programmi possono essere "risolti" (semplificati) proprio come delle operazione matematiche.

```haskell
filter odd [15,44,60,79,81,83]
filter odd [15,44,60,79,81,83] -- def. di filter
concat(map (test odd)[15,44,60,79,81,83]) -- map applica test odd
concat [test odd 15,test odd 44,test odd 60,
		test odd 79, test odd81, test odd83] -- map applica test odd 
concat [[15], [], [], [79], [81], [83]] -- applichiamo test odd
[15] ++ [] ++ [] ++ [79] ++ [81] ++ [83] -- applichiamo ++
[15,79,81,83]
```

