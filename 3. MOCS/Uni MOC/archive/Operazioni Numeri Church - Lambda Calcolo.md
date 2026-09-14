---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2026-07-13T11:16
updated: 2026-07-13T14:48
---
## Somma

```
succ = λx.λsz.s(xsz)
```

```
sum = λmn.λsz.ms(nsz)
```

```
sum a 1 = succ a
```

```
sum a 1 
	≡ λmn.λsz.ms(nsz) a 1
	→ λsz.as(1sz)
	≡ λsz.as(λxy.xy sz)
	→ λsz.as(sz)
	≡ λsz.as(sz)

succ a 
	≡ λx.λsz.s(xsz) a
	≡ λsz.s(asz)

sum 2 1 
	≡ λmn.λsz.ms(nsz) 2 1
	→ λsz.2s(1sz)
	≡ λsz.λfx.ffx s(λhy.hy sz)
	→ λsz.λfx.ffx s(sz)
	→ λsz.s(s(sz))
```



## Predecessore


