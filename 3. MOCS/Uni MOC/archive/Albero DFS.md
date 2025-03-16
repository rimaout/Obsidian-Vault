---
type: Uni Note
class:
  - "[[Algoritmi 2 (class)]]"
academic year: 2024/2025
related:
  - "[[Visita in profondità (DFS) - Grafi]]"
completed: true
created: 2025-03-06T18:48
updated: 2025-03-16T15:59
---
## Introduzione

Quando si utilizza l'*algoritmo DFS* per la visita di un grafo, i *nodi visitati* e gli *archi* effettivamente *attraversati* formano un albero detto **albero DFS**.

![[Pasted image 20250306175357.png|800]]

A sinistra un grafo `G`, a destra i tre alberi DFS che si ottengono facendo partire tre visite dai nodi `9`, `4`, `3` rispettivamente.

---
### Rappresentazione attraverso Vettore dei Padri

Un albero DFS può essere memorizzato tramite il vettore dei padri. Il vettore dei padri `P` di un albero DFS ha `n` elementi, dove `n` è il numero di nodi del grafo.

Se `i` è un nodo  dell'albero DFS allora:
- `P[i]` contiene il padre del nodo `i`.
- se `i` non è un nodo dell'albero, allora `P[i]` contiene `-1`.
- se `i` è la radice dell'albero allora `P[i]` contiene `i`.

![[Pasted image 20250306144000.png|550]]

>[!note] Algoritmo calcolo vettore dei padri
>
>Modificando lievemente la [[Visita in profondità (DFS) - Grafi|procedura DFS]] è possibile fare in modo che restituisca il vettore dei padri `P` anziché il vettore dei visitati.
>
>```python
>def Padri(u, G):
>	'''
>	genera il vettore dei padri `P` radicato nel nodo `u` dal grafo `G`
>	'''
>	n = len(G)
>	P = [-1]*n
>	P[u] = u    # segna `u` come radice
>	DFSr(u, G, P)
>	
>	return P
>```
>
>```python
>def DFSr(x, G, P):
>	for y in G[x]:
>		if P[y] == -1:
>			P[y] = x
>			DFSr(y, G, P)
>```

---
## Algoritmo Ricerca Cammino

Dato un grafo `G` in molte situazione vogliamo determinare un cammino che ci consenta di andare da un nodo `x` ad un nodo `y`.

Per fare ciò dobbiamo:
1. Generare il [[#Rappresentazione attraverso Vettore dei Padri|vettore dei padri]] `P` sul grafo `G` usando come radice il nodo `x`.
2. Vedere se `y` è raggiungibile controllando che `P[y] != -1`
3. Inseriamo il nodo `y` in path, poi troviamo il suo padre (che chiameremo `v`) in `P[y]` e lo inseriamo in path, procediamo trovando il padre di `v` in `P[v]` e lo inseriamo in path ripetiamo questo procedimento "inseguendo i padri" finche arriviamo alla radice `x`.
4. Il risultato sarà il percorso da `y` a `x`, che può essere letto al contrario per ottenere il cammino da `x` a `y`.

```python
def Cammino(u, P):
	if P[u] == -1: retunrn []
	path = []
	
	while P[u] != u:
		path.append(u)
		u = P[u]
	
	path.append(u)
	path.reverse()

	return path
```

>[!danger] Costo
>
>Disponendo del vettore dei padri, la complessità della procedura è $O(n)$. Perché nel caso peggiore il cammino sarà composto tutti i nodi del grafo.

>[!note] Implementazione Ricorsiva
>
>```python
>def Cammino(u, P):
>	if P[u] == -1: return []
>	if P[u] == u: return [u]
>	return CamminoR(P[u], P) + [u]
>```
>
>Anche in questo caso disponendo del vettore dei padri, la complessità della procedura è $O(n)$.

>**Cammino Minimo:** L'albero DFS *non assicura* di calcolare il cammino minimo per raggiungere un determinato nodo, per fare ciò dobbiamo utilizzare la [[Visita in profondità (DFS) - Grafi|visita in profondità (DFS)]].