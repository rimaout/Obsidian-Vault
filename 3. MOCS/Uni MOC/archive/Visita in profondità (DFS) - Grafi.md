---
type: Uni Note
class:
  - "[[Algoritmi 2 (class)]]"
academic year: 2024/2025
related: 
completed: true
created: 2025-03-06T17:14
updated: 2025-03-06T17:30
---
## Introduzione

Una visita profonda DFS (Depth-First Search) su un grafo è un algoritmo di ricerca che esplora il grafo visitando i nodi in profondità, cioè esplorando il più possibile lungo ogni ramo prima di tornare indietro.

Quando si vista un grafo è importante non andare in loop, ovvero non dobbiamo visitare più volte lo stesso nodo.

---
## Versione Matrice di Adiacenza

```python
def DFS(u, M)
	'''
	esegue visita dei nodi in nella matrice `M`
	raggiungibili a partire del nodu `u`
	'''
	
	n = len(M)           # costo: Θ(1)
	visitati = [0]*n     # costo: Θ(n)
	
	DFSr(u, M, visitati) # costo: ?
	return [x for x in range[n] if visitati[x]] # costo: Θ(n)
```

```python
def DFSr(u, M, visitati)
	'''
	segna come visitato il nodo `u` e richiama la funzione 
	su tutti i nodi addiacenti ancora non visitati 
	'''
	visitati[u] = 1                          # costo: Θ(1)
	for i in range(len(M)):                  # ripetuto `n` volte
		if M[u][i] == 1 and not visitati[i]: # costo: Θ(1)
			DFSr(i, M, visitati)             # costo: ?
```

>[!danger] Costo
>
>Abbiamo che la funzione `DFS` ha come costo $\Theta(n)$ (dovuto dalle creazione di visitati e del `ruturn`) a cui va sommato però il costo di `DFSr`.
>
>Il costo `DFSr` è influenzato dal `for` che si ripete $\Theta(n)$ volte e all interno ha una chiamata ricorsiva che nel peggiore dei casi avviene su tutti e `n` i nodi. 
>
>Quindi il costo complessivo di: 
>- `DFSr` è $\Theta(n) \times O(n) = O(n)$
>- `DFS` è $\Theta(n)$ + costo `DFSr` ovvero $\Theta(n) + \Theta(n^{2}) = \Theta(n^{2})$
>
>>***oss:*** `n` è la lunghezza della lista della matrice, ovvero è il numero di nodi del grafo.

---
## Versione Liste di Adiacenza

```python
def DFS(u, G):
	'''
	esegue visita dei nodi di G raggiungibili a partire dal nodo u
	'''

	n = len(G)              # costo: Θ(1)
	visitati = [0]*n        # costo: Θ(n)
	DSFr(u, G, visitati)    # costo: ?
	return [x for x in range(n) if visitati[x]] # costo: Θ(n)
```

```python
def DFS(u, G, visitati):
    visitati[u] = 1              # costo: Θ(1)
    for v in G[u]:               # ripetuto per il numero di archi di `u`
	    if not visitati[v]:      # costo: Θ(1)
			DFSr(v, G, visitati) # costo: ?
```

>[!danger] Costo
>
>Abbiamo che la funzione `DFS` ha come costo $\Theta(n)$ (dovuto dalle creazione di visitati e del `ruturn`) a cui va sommato però il costo di `DFSr`.  
>
>Il costo `DFSr` è influenzato dal `for` che si ripete tante volte quanti sono gli elementi nella lista `G[u]`, visto che in `G[u]` sono presenti tutti i nodi associati al nodo `u`. Possiamo di dire che il costo totale di tutte le chiamate ricorsive di `DFSr` nel peggiore dei casi (ovvero quando abbiamo un grafo connesso) è uguale ad `m` ovvero il numero di archi del grafo.
>
>Quindi il costo complessivo di: 
>- `DFSr` è  $O(m) = O(m)$
>- `DFS` è $\Theta(n)$ + costo `DFSr` ovvero $\Theta(n) + \Theta(m)$
>  
>>***oss:*** La complessità di spazio della procedura è $O(n)$

>[!warning] Versione Iterativa
>
>```python
>def DFSi(u, G):
>	'''
>	esegue visita dei nodi di G raggiungibili a partire dal nodo `u`
>	'''
>	
>	visitati = [0]*len(G)
>	pila = [u]   # inizializzazione della pila con il nodo di partenza
>	
>	while pila:
>		u = pila.pop()
>		if not visitati[u] = 1
>			# aggiungiamo i vicini non visitati
>			for v in G[u]:
>				if not visitati[v]:
>					pila.append(v)
>				
>	return [x for x in range(len(G)) if visitati[x]]
>```

---
## Algoritmo migliore

Per l’algoritmo DFS conviene utilizzare la versione con liste di adiacenza rispetto alla versione con matrice. Questo perché tramite le liste di adiacenza otteniamo un costo compreso tra $O(n)$ e $O(n^{2})$, infatti:

Nel **caso migliore** abbiamo un ***grafo sparso*** con $m = \Theta(n)$ e quindi otteniamo $\Theta(n) + \Theta(m) = \Theta(n)$

Nel **caso peggiore** abbiamo un ***grafo completo*** con  $m = n^{2}$ e quindi otteniamo $\Theta(n) + \Theta(m) = \Theta(n^{2})$

