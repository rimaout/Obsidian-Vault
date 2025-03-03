---
type: Uni Note
class:
  - "[[Algoritmi 2 (class)]]"
academic year: 2024/2025
related: 
completed: false
created: 2025-03-03T14:04
updated: 2025-03-03T15:16
---
## Visita in Profondità

Visita in profondità (DSF) su un grafo rappresentato tramite matrice di adiacenza.


è importante non andare in loop, ovvero non dobbiamo visitare più volte lo stesso percorso.

```python
def DFRs(u, M, visitati)
	'''
	segna come cisitato il nodo `u` e
	richiama la funzione su tutti i nodi addiacenti ancora non visitati 
	'''
	visitati[u] = 1
	for i in range(len(M)): 
		if M[u][i] == 1 and not visitati[i]:
			DFSr(i, M, visitati)
```

```python
def DFS(u, M)
	'''
	esegue fisita di nodi in `M` raggiungibili a partire del nodu `u`.
	'''
	
	n = len(M)
	visitati = [0]*n   # lista dei nodi visitati, inizializzata con `n` volte 0
	DFSr(u, M, visitati)
	retuen [x for x in range[n] if visitati[x]]
```

>[!danger] Costo
>
>adfjaljfdsljlk<
>
>Quindi il costo complessivo di questa operazione è $O(n) \times \Theta(n) = O(n^{2})$
>
>>***oss:*** `n` è la lunghezza della lista della matrice, ovvero è il numero di nodi del grafo.

>[!warning] Versione Iterativa

---

Versione con tramite liste di adiacenza, conviene perche costo finale è $O(n+m)$, infatti al massimo se il grafo è completo avremo che $m = n^{2}$ e che quindi il costo sia $O(n^{2})$ ma in tuti gli altri casi abbiamo un costo compreso tra $O(n)$ e $O(n^{2})$.

