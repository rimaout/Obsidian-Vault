---
Created: 2024-03-11
Type: Uni Note
Class:
  - "[[Introduzione agli Algoritmi (class)]]"
Academic Year: 2023/2024
Related: 
Completed: false
---
---

>[!info] Index
>1. 

---
**oss:** i programmi ricorsivi sono sempre meno efficienti rispetto ad algoritmi iterativi, per questo si usano i programmi ricorsivi soltanto quando sono molto più semplici da scrivere rispetto a programmi iterativi

per calcolare il costo di un programma ricorsivo dobbiamo:
1. Trovare equazione di ricorrenza
2. Risolvere equazione di ricorrenza

*Programma iterativo:*
```python
def fat(n):
	f=1

	for i in range(n+1):
	f *= i

	return f
```

Il costo temporal di questo programma ha costo $\Theta(n)$ il costo spaziale è $\Theta(1)$

*Programa ricorsivo:*

```python
def fat(n):
	if n<=1:
		return 1
	
	return fat((n-1)*n)
```

>[!warning] oss
>Ogni equazione di ricorrenza ha due casi
>- il caso base (caso finale)
>- e il caso ricorsivo 

$$
T(n) = \begin{cases}
T(n-1) + \Theta(1) \\
\Theta(1) &\text{if }n\leq 1 \ \ \ \textcolor{orange}{\text{caso base}}
\end{cases}
$$
il costo temporale di questo programma è $\Theta(n)$ e il costo spaziale è $\Theta(n)$
quindi conviene sempre le la versione iterativa anche a parità di costo temporale



---
```python
def ricSeqr(A, x):
	if A == []:
		return False
	
	if A[0] == x:
		return True

	return ricSeqR(A[1:], x)
```

Definiamo come $n$ il numero di elementi di A

*Costo temporale*
$$
T(n) = \begin{cases}
\Theta(1) &\text{if } n=0 \\
T(n-1)+\Theta(n) & \text{altrimenti}
\end{cases}
$$

*Costo Spaziale:*
il costo spaziale dipende dal numero dal numero di chiamate ricorsive (copie del programma) per il costo spaziale del singolo programma di base

nel caso di questo programma
- ogni volta che facciamo una chiamata ricorsiva la grandezza della array diminuisce di uno quindi il costo è:
$$
\Theta\left( \sum^{n}_{i=1} \Theta(i) \right)
$$

Dove $\sum^{n}_{i=1} \Theta(i)$ descrive il costo dell’array dove $i$ rappresenta il numero di elementi dell'array q

Quindi il caso in cui:
- $i=n$ è il caso iniziale in cui l'array ha ancora tutti gli elementi  
- $i=0$ è il caso finale quando l'array è vuoto

---
## Versione più efficiente del programma di prima

```python
def ricSeqr(A, x, i=0):
	if i >= len(A):
		return False
	
	if A[i] == x:
		return True

	return ricSeqR(A, x, i+1)
```

- Facendo cosi abbiamo rimosso lo slicing (riduzione costo temporale)
- E abbiamo ridotto anche il costo spaziale infatti ogni volta che effettuiamo una chiamata ricorsiva non salviamo  una nuova copia dell'array ma passiamo un puntatore alla array originale

---
## Ricerca binaria ricorsiva

```python
def ricBinR(A, x, i=0, j=False:

	if j == False:
		j = len(A)

	if i>j:
		return False
		
	m = (i+j)//2
	if A[m] == x:
		return True
	
	if A[m] > x:
		return ricBinR(A, x, i, m-1)
	
	return ricBinR(A, x, m+1, j)
```

---
## Fibonacci
**Iterativo:**

```python
def Fib(n)
 if n<=1 :
	 return n

a,b = 0,1
for i in range(2, n+1):
	a, b = b, a+b

return b

```

**Ricorsivo:**

```python
def fibR(n):
	if n<=1:
		return n
	
	return fibR(n-1) + fibR(n-2)
```

Equazione Ricorrenze:
$$
T(n) = \begin{cases} 
\Theta(1) & \text{if }n\leq 1\ \ \ \ \ \  \textcolor{orange}{\text{caso base}}\\

T(n-1)+ T(n-2) + \Theta(1) &\text{altrimenti}
\end{cases}
$$
---
