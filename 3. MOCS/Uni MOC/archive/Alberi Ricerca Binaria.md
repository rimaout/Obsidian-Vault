---
created: 2024-05-06T12:12
type: Uni Note
class: 
academic year: 2023/2024
related: 
completed: false
updated: 2024-05-27T13:29
---
---

>[!abstract] Index
>1. 

>[!abstract] Related
>- 

---

## Alberi Ricerca Binaria

>[!info] Costi
>- Ricerca: $O(n)$
>- Inserimento: $O(n)$
>- Cancellazione: $O(n)$

**oss:** se albero è bilanciato allora h = $\log n$


In un albero di ricerca se un nodo a un valore x
- il nodo si sinistra ha valore minore di x
- il nodo di destra ha un valore maggiore di x

>[!info] Struttura
>
>```python
>def nodoABR() :
>	
>```

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

#### Cancellazione 
1. Trovare elemento

possono accadere 4 cose:
- x non appartiene all'albero (non devo fare niente)
- x è una foglia (elimino l'elemento)
- x è un nodo padre con un unico figlio (allora faccio puntare il nodo padre di x al unico nodo figlio di x)
- x è un nodo padre con due figli: 
	- innesco un iterazione dove sostituisco il valore di x con il valore del figlio sinistro
	- Effettuo un nuova cancellazione sul figlio sinistro di x (e il processo si ripete fino a quando non raggiungo una foglia o un nodo con un singolo figlio)

```python
def canc(p, x):
    # Se l'albero è vuoto, ritorna None
    if p == None: 
        return p

    # Se l'albero ha un solo elemento (la radice) che è uguale a x, ritorna None
    if p.key == x and p.left == p.right == None:   
        return None

    # Se la radice è uguale a x e ha solo un figlio destro, sostituisci la radice con il figlio destro
    if p.key == x and p.left == None:
        p.right.parent = None
        return p.right

    # Se la radice è uguale a x e ha solo un figlio sinistro, sostituisci la radice con il figlio sinistro
    if p.key == x and p.right == None:
        p.left.parent = None
        return p.left

    # Cerca il nodo con chiave x
    q = p
    while q != None and q.key != x:
        if x < q.key: 
            q = q.left
        else: 
            q = q.right

    # Se il nodo con chiave x non è stato trovato, ritorna l'albero originale
    if q == None: 
        return p

    # Se il nodo con chiave x ha entrambi i figli, sostituisci la chiave del nodo con la chiave del figlio sinistro
    while q.left != None and q.right != None:
        q.key = q.left.key
        q = q.left

    s = None
    # Se il nodo da eliminare ha un figlio sinistro, imposta s come il figlio sinistro
    if q.left != None:
        s = q.left
        s.parent = q.parent

    # Se il nodo da eliminare ha un figlio destro, imposta s come il figlio destro
    if q.right != None:
        s = q.right
        s.parent = q.parent 

    # Se il nodo da eliminare è il figlio sinistro del suo genitore, sostituisci il figlio sinistro del genitore con s
    if q.parent.left == q:
        q.parent.left = s
    else:
        # Se il nodo da eliminare non è il figlio sinistro del suo genitore, sostituisci il figlio destro del genitore con s
        q.parent.right = s

    # Ritorna la radice dell'albero
    return p
```

>[!warning] Esempio Chiamata
>
>```python
> p = canc(p, x) # p è il puntatore a radice, x è l'elemento da cercare
>```

