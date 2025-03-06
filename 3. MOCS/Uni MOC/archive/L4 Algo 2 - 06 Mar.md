---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-03-06T14:13
updated: 2025-03-06T18:47
---
# Colorazione dei Grafi 

[[Colorazione dei Grafi]]

non posso avere due nodi co lo stesso colore se sono addiacenti:

il numero massimo di coloiri è `n` dove `n` è il numero di nodi (grafo completo)

numero minimo di colori è `1` (caso grafo senza archi)


oss se c'è un ciclo composto da un ciclo di numero dispari di nodi allora sicuramente non può essere colorato con due grafi.

Un grafo è bi-colorabile se non contiene cicli di numero dispari di nodi.

```python
def Colora(G):

	Colore = [-1]*len(G)
	DFSr(0, G, Colore, 0)
	return Colore
```

```python
def DFSr(x, G, Colore, c):
	Colore[x] = c
	for y in G[x]:
		if Colore[y] ==- 1:
	
```

questo non funziona bene per cicli dispari, questa altra versione controlla ...:

```pyhton

```


# Componente Connessa


## Componente fortemente conessa

