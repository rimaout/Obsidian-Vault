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

## Esercizio tipo esame

traccia ...

```python
def trovato(x, P):
	if P == None:
		return False

	while P != None:
		if p.key ==x:
			return True
		p = p.next
	return False
```

## Metodo mio (costo spaziale O(n))

```python
def intersezione(P1, P2) :
	P3 = None

	while P1 != None:
		if trovato(P1.key, P2) and not trovato(P1.key, p3):

			if P3 == None:
				P3 = Nodo(p1.key):
				q = P3
			
			else:
				q.next = Nodo(p1.key)
				q = q.next
		
		P1 = P1.next
```

## Metodo prof (costo spaziale O(n))

```python
def intersezione(P1, P2) :
	P3 = None

	while P1 != None:
		if trovato(P1.key, P2) and not trovato(P1.key, P3):
			P3 = Nodo(p1.key, P3)
		
		P1 = P1.next
```

## Metodo Prod (costo spaziale O(1))

```python
 
```

>[!warning] il costo temporale di tutti questi casi è O(n^2)

---
## Alberi


**Albero binario completo:**
per essere completo un albero deve avere tutti i noti con due figli (0 se i nodi sono foglie) e deve avere tutte le foglie allo stesso livello

**Albero quais completo:**
un albero binario si dice quasi completo quando le fogli e sono a livelli addicenti (forse è giusto)


**altezza**
- l'altezza di un albero è il numero di livelli
- l'altezza è il numero passaggi massimo (caso peggiore) necessario per raggiunger un qualsiasi nodo


**albero sbilanciato** vs **albero bilanciato**

**Costruttore nodo:**
```python
class NodoAB:
	def _init_(self, key = None, left = None, right = None):
		self.key = key
		self.left = left
		self.right = right
```

