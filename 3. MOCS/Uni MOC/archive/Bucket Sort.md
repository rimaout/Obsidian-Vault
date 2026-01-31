---
created: 2024-04-30T17:17
type: Uni Note
class:
academic year: 2023/2024
related:
completed: false
updated: 2026-01-31T13:32
---
---

>[!abstract] Index
>1. 

>[!abstract] Related
>- 

---
## Bucket Sort

```python
def boo(A,k):
	B = [[] for _ in range(k)] # creo k secchi    θ(k) = O(n)
	m = max(A) # θ(n)
	
	for x in A             #
		i = x * k // (m+1) # θ(n)
		B[i].append(x)     #

	for i in range(k): #
		B[i].sort()    # θ(?)
		
	C = []             #
	for i in range(k): # θ(n)
		C.extend(B[i]) #

	return C
```

**Costo secondo for:** $\sum^{k-1}_{i=0}\text{costo di ordinamento}(B[i])$


>[!info] Quando 
>Il bucket sort funziona bene se il numeri sono equi distribuiti su tutto l'intervallo e se non ci sono molte ripetizioni
