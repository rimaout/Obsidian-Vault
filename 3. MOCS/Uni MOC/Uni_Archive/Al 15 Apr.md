---
Created: ""
Type: Uni Note
Class: 
Academic Year: 2023/2024
Related: 
Completed: false
---
---

>[!info] Page Index
>1. 

>[!info] Related Content
>- 

---

[[Heap (Struttura Dati)]]

```python
def heapfy1(H, i) //A = array, i = ?
	L = 2i+1
	R = 2i+2
	min = i

	if l < len(A) and A(L) < A(i):
		min = L

	if R < len(A) and H(R) < H(min):
		min = R

	if min != i:
		A[i], A[min] = A[min], H[i]
		heapfy1(H, min)
```

## Counting Sort

```python
def CountSort(A):
	n = len(A)
	M = max(A)
	C = [0]*(M+1)
	for x in A:
		c[x]+1
	B=[]
```

---