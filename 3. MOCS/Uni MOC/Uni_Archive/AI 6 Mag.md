---
Created: ""
Type: Uni Note
Class: 
Academic Year: 2023/2024
Related: 
Completed: false
---
---

>[!abstract] Index
>1. 

>[!abstract] Related
>- 

---

>[!info] Costi
>- Ricerca: $O(n)$
>- Inserimento: $O(n)$
>- Cancellazione: $O(n)$

**oss:** se albero è bilanciato allora h = $\log n$


In un albero di ricerca se un nodo a un valore x
- il nodo si sinistra ha valore minore di x
- il nodo di destra ha un valore maggiore di x


#### Ricerca
Costo ricerca: $T(h)\leq T(h-1)+\Theta(1)$

```python
def ricerca(p, x):
	if p == None: return false

	if p.key == x: return True

	if x < p.key: return ricerca(p.left, x)

	return ricerca(p.right, x)
```

il miglior modo per stampare un albero in ricerca binaria è utilizzare la stampa pre order

Ricerca massimo:
- vado sempre a destra fino a quando non arrivo a un nodo senza figlio destra


Esercizi x casa:
- Trovare predecessore ovvero il più grande degli elementi più piccoli di x
- Trovare successore ovvero più piccolo degli elementi più grandi di x 

#### Inserimento 
```python
def inserimento(p, x):
	z = NodoABR(x)
	
	if p == None: 
		return z

		q=p
		while p != None:
			if x < p.key: p=p.left
			
			elif x == p.key: return q

			else: p = p.right

	return q
```
