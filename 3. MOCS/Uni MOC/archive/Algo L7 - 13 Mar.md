---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-03-13T16:09
updated: 2025-03-16T12:56
---

# Visita in Ampiezza BFS

La visita in ampiezza (Breadth First Search) esplora i nodi del grafo partendo da quelli a distanza 1 da un nodo iniziale `x`. Poi visita quelli a distanza 2 e così via.

>***oss:*** L’algoritmo visita tutti i vertici a livello `k` prima di passare a quelli a livello `k+1`.

![[Screenshot 2025-03-13 at 17.35.04.png|600]]

### Algoritmo 

```python
def BFS(x, G):
	'''
	restituisce i nodi raggiungibili da `x`.
	'''
	visitati = [0]*len(G)
	visitati[x] = 1
	
	coda = [x]
		while coda:        # finche coda non è vuota
		u = coda.pop(0)    # rimuovi 1° elemento
		for y in G[u]:
			if visitati[y] == 0:
			visitatu [y] = 1
			# nota che y va in coda solo se non visitato
			coda.append(y)
	return visitati
```

coda.pop può costare O(n) male male

metti l'altro algoritmo con cancellazione logica, riscrivili sostituendo la `i` con `testa` per far capire che "cancelliamo" i primi nodi della coda spostano l'inzzio in avanti.



## Albero BFS

La visita in ampiezza genera un albero, che rappresenta i cammini minimi per tutti i nodi raggiungibili partendo da un nodo iniziale `x`.

![[Pasted image 20250313173928.png|800]]