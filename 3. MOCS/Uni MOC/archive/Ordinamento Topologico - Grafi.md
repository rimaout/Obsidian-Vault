---
type: Uni Note
class:
  - "[[Algoritmi 2 (class)]]"
academic year: 2024/2025
related: 
completed: true
created: 2025-03-07T14:09
updated: 2025-03-27T11:44
---
## Introduzione

Spesso un grafo diretto è utilizzati per catturare relazioni di propedeuticità, ad esempio un arco da `a` a `b` può essere utilizzati per indicare che `a` è propedeutico a `b`.

Un grafo si dice che **rispetta tutte le propedeuticità** se è possibile ordinarlo in modo tale che gli archi vadano tutti da sinistra verso destra. Questo ordinamento è dotto **ordinamento topologico**.

![[Pasted image 20250308163932.png|900]]

Un grafo diretto può avere da `0` ad `n!` ordinamenti topologici.

>***oss:*** Più archi ha un grafo minore sarà il numero di ordinamenti topologici possibili, infatti il grafo con il maggior numero di di ordinamenti topologici è un grafo senza archi, con n! ordinamenti topologici.

## DAG (direct acyclic graph)

Un grafo ha un ***ordinamento topologico*** se è un **DAG**, ovvero un grafo diretto aciclico.

La presenza di un ciclo nel grafo implica che nessuno dei nodi del ciclo possa comparire nell’ordine giusto. Ognuno di essi richiede di apparire nell’ordinamento alla destra di chi lo precede.

>***oss:*** Un grafo DAG ha sempre un [[Introduzione Grafi#^e35772|nodo sorgente]].

## Algoritmi per trovare ordine topologico.

```python
def sortTopo(G):
	'''
	Restituisce un sort topologico di G se esiste
	altrimenti restituisce la lista vuota
	'''
	
	# calolo grado entrante nodi
	gradoEnt = [0] * len(G)
	for i in range(len(G)):
		for j in G[i]:
			gradoEnt[j] += 1
	
	# calcolo sorgenti
	sorgenti = [i for i in range(len(G)) if gradoEnt[i]==0]
	
	# ordinamento topologico
	ST = []
	while len(sorgenti) != 0:
		u = sorgenti.pop()
		ST.append(u)
		for v in G[u]:
			gradoEnt[v] -= 1
			if gradoEnt[v] == 0:
				sorgenti.append(v)
	
	if len(ST) == len(G): 
		return ST
	else:
		return []
```

>[!danger] Costo Computazionale
>
>- L’inizializzazione del vettore dei gradi entranti ha come costo $O(n + m)$.
>- L'inizializzazione dell’insieme delle sorgenti ha come costo $O(n)$.
>- Il `while` viene iterato $O(n)$ volte e il costo totale del `for` al termine del `while` è $O(m)$.
>  
>Quindi il costo totale finale è $O(n + m)$.

>[!note] Versione DFS
>
>```python
>def sortTopo(G):
>	'''
>	restituisce sort toppologico del
>	grafo aciclico G
>	'''
>	
>	visitati = [0]*len(G)
>	lista = []
>	
>	for u in range(len(G)):
>		if visitati[u] == 0:
>			DFSr(u, G, visitati, lista)
>			
>	lista.reverse()
>	return lista
>```
>
>```python
>def DFSr(u, G, visitati, lista):
>	visitati[u] = 1
>	for v in G[u]:
>		if visitati[v] == 0:
>			DFSr(v, G, visitati, lista)
>	lista.append(u)
>```