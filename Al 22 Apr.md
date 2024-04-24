---
Created: 2024-04-22
Type: Uni Note
Class:
  - "[[Introduzione agli Algoritmi (class)]]"
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
## Bucket Sort

```python
def boo(A,k):
	B = [[] for _ in range(k)] # creo k secchi    θ(k) = O(n)
	m = max(A) # θ(n)
	
	for x in A             #
		i = x * k // (m+1) # θ(n)
		B[i].append(x)     #

	for i in range(k): #
		B[i].sort()    # θ(?)
		
	C = []             #
	for i in range(k): # θ(n)
		C.extend(B[i]) #

	return C
```

**Costo secondo for:** $\sum^{k-1}_{i=0}\text{costo di ordinamento}(B[i])$


>[!info] Quando 
>Il bucket sort funziona bene se il numeri sono equi distribuiti su tutto l'intervallo e se non ci sono molte ripetizioni


---

## Pila
First in last out

- **Insert:** $\theta(1)$
- **Cancellazione:** $\theta(1)$


##### Implementazione con lista python

```python
def ins(Pila, x):
	Pila.append(x)
```
- costo: $\theta(1)$

```python
def canc(Pila):
	return Pila.pop()
```
- costo: $\theta(1)$

##### Implementazione con linked list


---
## Coda
first in first out

- **Insert:** $\Theta(1)$
- **Cancellazione:** $\theta(1)$

##### Implementazione con lista python

```python
def ins(Coda, x):
	Coda.append(x)
```
- costo: $\theta(1)$

```python
def canc(Coda):
	if Coda == []: 
		return None
	#else
	return Coda.pop(0)
```
- costo: $\theta(n)$

##### Implementazione con linked list

**Inserimento**
procedura per inserire in lista non vuota:
- Creare nuovo elemento
- far puntare il campo next dell’elemento in coda al nuovo elemento
- far puntare il puntatore coda al nuovo elemento

procedura per inserire in lista vuota:
- Creare nuovo elemento
- far puntare il puntatore testa al nuovo elemento
- far puntare il puntatore coda al nuovo elemento

codice:
```python
def ins(testa, coda, x):
	# funione che inserisce un elemnto (x) in coda 
	# e ritorna il punatore all'primo elemento (test) e all'ultimo coda)

	p = Nodo(x)
	if coda = None:    # se lista vuota
		return p, p

	coda.next=p
	return testa, P

```


**Cancellazione**
procedura:
1. Estrarre elemento puntato dal puntatore testa 
2. Far puntare puntatore testa al elemento puntato dal campo nest del elemento puntato dal puntatore testa 
3. cancellare vecchio primo elemento (in python non serve)

```python
def canc(testa, coda):
	# funzione che cancella primo elemento
	# e ritorna valore cancellato, nuova testa, coda
	
	if testa == None:
		return None ,None, None
	
	if testa == coda:
		return testa.key, none, none

	return testa.key, testa.next, coda
```

>[!warning] In Python
>se vuoi usare una lista a puntatori in python puoi usare
>`from collections import deque`
>
>**Metodi:**
>```pyton
>A = deque([])   # θ(1)
>A.pop(x)           # θ(1)
>A.popleft()       # θ(1)
>A.popright()     # θ(1)
>A[x]                   # θ(x)
>```

---
