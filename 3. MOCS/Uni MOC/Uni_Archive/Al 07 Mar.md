---
Created: 2024-03-07
Type: Uni Note
Class:
  - "[[Algoritmi (class)]]"
Academic Year: 2023/2024
Related: 
Completed: false
---
---

>[!info] Index
>1. 

---
**Esempio 1:**

```python
def es(n):
	t=0      # O(1)
	n=abs(n) # O(1)
	
	if n>100:
		return 1 # O(1)

	for i in range(n)
		t += 3   # O(1)

return t         # O(1)
```

- Quando $n$ è minore di 100 allora il programma ha costo che dipende da $n$
	- ma $n$ in questo caso non sarà mai più grande di 100
- Quando $n$ tende a infinito allora il costo del programma è costante 

Quindi il costo di questo programma è $\Theta(1)$

---
**Esempio 2:**

```python
def es2(n):
	
	if n<0:   # O(1)
		n=-n  # O(1)
	# n è sempra positivo

	while n>0:
		if n%2==1:
			return 1  # O(1)
		n-=2  # O(1)
	
	return 0  # O(1)
```

se $n$ è
- dispari:
	- Programma termina subito una volta entrati nel while
	- costo $O(1)$
- pari:
	- while viene ripetuto $\frac{n}{2}$ infatti $n$ diminuisce di 2 ogni volta che si ripete il while
	- quindi costo $O(n)$

---
**Esercizio 3**

```python
def es3(n):
	n = abs(n)    # O(1)
	x = 0         # O(1)
	r = 0         # O(1)

	while x**2 < n:
		x += 1        # O(1)
		r += 3 * x    # O(1)

	return r    # O(1)
```

- programma finisce quando 
$$
\begin{align}
&x^{2} =n \\
&x =\sqrt{ n }
\end{align}
$$
- quindi il programma viene ripetuto $\sqrt{ n }$ volte

---
**Esercizio 4:**

```python
def es(n):
	n = abs(n)    # O(1)
	x = 0         # O(1)
	r = 0         # O(1)

	while n > 1:
		r += 2        # O(1)
		n = n//2      # O(1)

	return r    # O(1)
```

---
**Esercizio 5:**

```python
def es4(n)
	n = abs(n)
	p = 2

	while n > p:
		p = p*p

	return p
```


se n < 2 costo costante
se n >2 costo:
- programma finisce quando n = p
- p cresce in questo modo:
	- 2  --> 2^2 --> 4^2 --> 16^2 --> ... 
	- 2  --> 2^2 --> 2^4 --> 2^8   --> ...

- Quindi:
$$
\begin{align}
&2^{2^{i}} \\
continua
\end{align}
$$
---
**Esercizio 6:**

```python
def es(n):
	n = abs(n)
	t = 1
	x = 1

	for i in range(n): # O(n)
		t = 3t   # O(1)
	
	# oss: t = 3^n

	while t > x:
		x += 2
		t -= 2
	# oss uguale a scrivere x += 4 e t -= 0
	
	return t
```

3
9
27

t > x

3^n > x


3^n -2i > x +2i


3^n = x+4\*i


3^n-x = 4i

---
## Algoritmi di ricerca

**Base:**
```python
def R(array, elem)
	for i in range(len(array)):
		if array[i]==x:
			return i
	
	return None
```

caso peggiore: $O(n)$
caso migliore: $\Omega(1)$
caso medio: $\frac{n}{1}$ ovvero $O(n)$

---
