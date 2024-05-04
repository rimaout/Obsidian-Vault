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
**Nodo Albero Binario:**
```python
def NodoAB():
	
```


**Crea albero binario:**
```python
def creaAB(n, m) :
	if n==0: return None

	p = NodoA(random.randint(1, m))
	fs = random.randint(0, n-1)
	

```
Funzione che crea un albero di n nodi con dei valori presi casualmente tra 1 e m

**Esempio creazione albero binario:**
```python
p = creaA(n, m) # p puntatore a radice
```

**Stampa albero binario:**
```python
def stampaAB(p):
	if p==None: return None

	print(p.key)   # Stampa Nodo Padre
	print(p.left)  # Stampa Ramo Sinistro
	print(p.right) # Stampa Ramo Destro
```
Metodo chiamato PreOrder

```python
def stampaAB(p):
	if p==None: return None

	print(p.left)  # Stampa Ramo Sinistro
	print(p.key)   # Stampa Nodo Padre
	print(p.right) # Stampa Ramo Destro
```
Metodo chiamato InOrder

```python
def stampaAB(p):
	if p==None: return None

	print(p.left)  # Stampa Ramo Sinistro
	print(p.right) # Stampa Ramo Destro
	print(p.key)   # Stampa Nodo Padre
```
Metodo chiamato PostOrder

>[!warning] oss
>- Conteggio degli elementi conviene in PostOrder
>- Ricerca di un elemento conviene  in PreOrder


**Stampa leggermente più avanzata:**
```python
def StampaAB(p, h=0):
	if p==None: 
		print('|' * h, '-')
		return None

	print('|' * h, p.key)
	stampaAB(p.left, h+1)
	stampaAB(p.right, h+1)
```
- h indica il livello della ricorsione (si parte da 0)

>[!warning] Costo visita o stampa
>Costo di stampa o visita è $O(n)$

---

$T(n) = T(k)+ T(n-1-k)+\Theta(1)$ per $0\leq k\leq n-1$


Fai esempi casi estremi quindi con albero completamente bilanciato e albero completamente sbilanciato 
- Albero perfettamente bilanciato $T(n) = 2T\left( \frac{n}{2} \right)+\Theta(1)$
- Albero completamente sbilanciato $T(n)=T(n-1)+\Theta(1)$

per albero completamente sbilanciato si intende albero con tutti in nodi a sinistra o destra (ovvero albero in cui l'altezza è uguale al numero di nodi)

---
**Risolvere eq di ricorrenza:**
$$
T(n) = \begin{cases}
T(k)+T(n-k-1) + \Theta(1) & \text{se}  \\
T(1) & \text{se}
\end{cases}
$$

Metodo Sostituzione:
- $T(n) = T(k)+T(n-k-1) + b$
- - $T(1) = a$

Ipotesi: $T(n) \in \Theta(n)$ ovvero:
- $T(n)\leq c\cdot n$ ($O$)
- $T(n)\geq c\cdot n$ ($\Omega$)

Caso Base: $T(1) = a\leq c\cdot n$ vera per $c\geq a$

- $T(n)\leq c\cdot k+c(n-1-k)+b = c \cdot k+c\cdot n-c-ck+b$
- jslkvjkljklfs

**Esercizi:**

```python
def contaNodiAB(p):

	if p==None:
		return 0

	return 1 + contaNodiAB(p.left) + contaNodiAB(p.right)
	
	
```

```python
def RicercaLineareAB(p, x):
	if p==None: return False

	if p.key==x: return True

	if RecercaLineareAB(p.left, x): 
		return True
	else: 
		return RicercaLineareAB(p.right, x)
```

Altezza Albero Binario
```python
def AltezzaAB(p, x):
	if P==None: return -1 # caso in cui puntatore a None (non esiste radice)

	hs = Altezza(p.left)    # Altezza ramo sinistro
	hr = Altezza(p.right)   # Altezza ramo destro 

	return max(hs, hd) + 1
```

Contare numero di nodi in un determinato livello:
```python
def nodiLivello(p, k): # p = puntatore albero, k = livello
	if p==None: return 0

	if k==0: return 1

	return nodilivello(p.left, k-1) + nodilivello(p.right, k-1)
```

Stampa per livelli:
- usare coda
- Costo: $\Theta(n)$
- 