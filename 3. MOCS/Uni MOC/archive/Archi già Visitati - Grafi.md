---
type: Uni Note
class:
  - "[[Algoritmi 2 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-03-11T10:01
updated: 2026-01-31T13:32
---
## Definizioni

Durante la visita **DFS** di un grafo diretto posso incontrare nodi già visitati in tre modi diversi:

- **archi in avanti:** archi che collegano un antenato ad un discendente.
- **archi all’indietro** archi che collegano un discendente ad un antenato.
- **archi di attraversamento** archi che collegano nodi di due sotto alberi diversi, possiamo vederli come dei cugini che hanno un antenato in comune.

>[!example] Esempio
>
>![[Screenshot 2025-03-11 at 09.55.18.png|600]]
>
>>***oss:*** gli archi in grassetto sono gli *archi in avanti*, ovvero che collegano un nodo `a` ad un nodo `b`, dove `b` non era stato ancora visitato.

## Esercizio Ricerca Ciclo

Dato un grafo `G` (diretto o non diretto) ed un suo nodo `u`, vogliamo sapere se da `u` è possibile raggiungere un ciclo in `G`.

Per ricercare un ciclo all'interno del grafo possiamo sfruttare le definizioni appena viste. Infatti un grafo ha un ciclo se e solo se è presente un **arco all’indietro**.

Idea generale, creiamo un vettore `V` dei visitati che:
- `V[x] = 0` se il nodo `x` non è stato ancora visitato.
- `V[x] = 1` se il nodo `x` è stato visitato, ma la ricorsione in `x` *non* è ancora finita.
- `V[x] = 2` se il nodo `x` è stato visitato e la ricorsione in `x` è finita.

In questo modo scopro un ciclo quando trovo un arco diretto verso un nodo già visitato che si trova nello stato 1.

### Algoritmo

>[!note] Ciclo raggiungibile da un nodo `u`
>
>
>
>```python
>def ciclo(u, G):
>	'''
>	Ritorna true se esiste un ciclo in `G` raggiungibile dal nodo `u`.
>	'''
>	visitati  = [0]*len(G)
>	return DFSr(u, G, visitati)
>```

>[!note] Esiste un ciclo
>
>```python
>def ciclo(G):
>	'''
>	Ritorna true se è presente un ciclo nel grafo `G`
>	'''
>	
>	visitati = [0]*len(G)
>	
>	for u in range(len(G)):
>		if visitati[u] == 0:
>			if DFSr(u, G, visitati)
>				return True
>	return False
>```

```python
def DFSr(u, G, visitati):
	'''
	Restituisce True se la DFS da `u` trova un ciclo (arco indiretto)
	'''
	
	visitati[u] = 1
	for v in G[u]:
		if visitati[v] == 1:
			# Nodo in stato di elaborazione -> ciclo trovato
			return True
		if visitati[v] == 0:
			# Nodo non visitato, continua DFS
			if DFSr(v, G, visitati):
				return True

	visitati[u] = 2 # Nodo completamente esplorato
	return DFSr(u, G, visitati)
```

