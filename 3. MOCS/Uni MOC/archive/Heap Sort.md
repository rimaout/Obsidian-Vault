---
created: 2024-04-11
type: Uni Note
class:
  - "[[Introduzione agli Algoritmi (class)]]"
academic year: 2023/2024
related:
  - "[[Heap (Struttura Dati)]]"
completed: false
updated: 2024-05-27T13:29
---
---

>[!info] Index
>1. 

---

```Python
from heapq import heapfy, heappoo

def heapSort(A):
	heapfy() //O(n)
	B=[]

	while len(a)>0:
		B.append(heappop(A)) //O(log n)
	return B

```

**Costo Algoritmo:**
- il while viene ripetuto `n` volte (dove n è la lunghezza dell'array)
- Quindi costo del while `n * O(log n) = O(n log n)`
- Costo programma è costo `heapfy() + costo while` = `O(n) + O(n log n) = O(n log n)`

---