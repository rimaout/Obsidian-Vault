---
Created: 2024-03-07
Type: Uni Note
Class:
  - "[[Algoritmi 1 (class)]]"
Academic Year: 2023/2024
Related: 
Completed: false
share_link: https://share.note.sx/0apkrtqy#9bNxrxWIiba9EvCKsOZ2VLIS0worQdvJPHI7tPpdL8I
share_updated: 2024-03-11T08:58:11+01:00
---
c---

>[!info] Index
>1. 

---
**Esempio 0:**

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
**Esempio 1:**

```python
def es1(n):
	
	if n<0:   # O(1)
		n=-n  # O(1)
	# n è sempre positivo

	while n>0:
		if n%2==1:
			return 1  # O(1)
		n-=2  # O(1)
	
	return 0  # O(1)
```

$O(\frac{n}{2})$ --> $O(n)$ (pari)
$\Omega(1)$ (dispari)

se $n$ è
- dispari:
	- Programma termina subito una volta entrati nel while
	- costo $O(1)$
- pari:
	- while viene ripetuto $\frac{n}{2}$ infatti $n$ diminuisce di 2 ogni volta che si ripete il while
	- quindi costo $O(n)$

---
**Esercizio 2**

```python
def es2(n):
	n = abs(n)    # O(1)
	x = 0         # O(1)
	r = 0         # O(1)

	while x**2 < n:
		x += 1        # O(1)
		r += 3 * x    # O(1)

	return r    # O(1)
```

**Calcoli:**

1. $(i-1)^{2} = n$
2. $i^{2}-2i+1=n$    $\sim$    $i^{2}=n$ 
3. $i = \sqrt{ n }$

*costo:* $\Theta(\sqrt{ n })$

*oss:* $\sqrt{ n }\not\sim n$

---
**Esercizio 3:**

```python
def es3(n):
	n = abs(n)    # O(1)
	x = 0         # O(1)
	r = 0         # O(1)

	while n > 1:
		r += 2        # O(1)
		n = n//2      # O(1)

	return r    # O(1)
```

| Iterazione | valore di n | Operazione  |
| ---------- | ----------- | ----------- |
| 0          | 16          | n           |
| 1          | 8           | n/2         |
| 2          | 4           | (n/2)/2     |
| 3          | 2           | ((n/2)/2)/2 |

*oss:*  $\text{operazione}=\frac{n}{2^{\text{iterazione}}}$ ovvero $\frac{n}{2^{i}}$
*oss:* "usciamo" del programma quando $n=1$

*calcoli:*
1. $\frac{n}{2^{i}} = 1$ 
2. $2^{i}=n$ 
3. $\log_{2}2^{i}=\log_{2}n$   (oss: posso scegliere la base più comoda)
4. $i\cdot \log_{2}2=\log_{2}n$
5. $i\cdot 1=\log n$
6. $i=\log n$

Quindi costo programma è $\Theta(\log n)$

---
**Esercizio 4:**

```python
def es4(n)
	n = abs(n)
	p = 2

	while n > p:
		p = p*p  

	return p
```

Caso migliore: se n < 2 allora costo è costante --> $\Theta(1)$

se n > 2 allora:

rappresentazione while con valore di n casuale (n=30):

| Iterazione | valore di n | Operazione                 | valore di p |
| ---------- | ----------- | -------------------------- | ----------- |
| 0          | 30          | $p=2$                      | 2           |
| 1          | 30          | $p^{2}$                    | 4           |
| 2          | 30          | ${p^{2}}^{2} = p^{4}$      | 16          |
| 3          | 30          | ${{p^{2}}^{2}}^{2} =p^{8}$ | 256         |

*oss:* $p^{2^{i}}$ e $p=2$

1. ${2^{2}}^{i}=n$
2. $\log_{2}{2^{2}}^{i}=\log_{2} n$
3. $2^{i}\cdot\log_{2}2=\log_{2}n$
4. $2^{i} = \log_{2}n$
5. $\log_{2}2^{i} = \log_{2}(\log_{2}n)$
6. $i\cdot\log_{2}2 = \log_{2}(\log_{2}n)$
7. $i = \log_{2}(\log_{2}n)$

*Quindi costo programma:* $O(\log (\log n))$

---
**Esercizio 4:**

```python
def es4(n):
	n = abs(n)
	t = 1
	x = 0

	for i in range(n): # O(n)
		t = 3*t   # O(1)
	
	# oss: t = 3^n

	while t > x:
		x += 2
		t -= 2
	# oss uguale a scrivere x += 4 e t -= 0
	
	return t
```

- Complessità primo for è $\Theta(n)$
- Alla fine del for $t = 3^{n}$

Visualizzazione while
0. $t-2\cdot i=x+2\cdot i$  
1. $3^{n}-2\cdot i = 0 + 2\cdot i$
2. $3^{n}=2\cdot{i}+2\cdot{i}$
3. $3^{n} = 4\cdot i$
4. $\frac{3^{n}}{4}=i$ 
5. $3^{n} = i$

Quindi complessità while è $\Theta(3^{n})$
Quindi la complessità generale del programma è $\Theta(3^{n})+\Theta(n) \sim \Theta(3^{n})$ 
Dove $\Theta(n)$ + a complessità del primo for

**Esercizio 6:**

```python
def es7(n):
	n=abs(n) #O(1)
	u=1      #O(1)
	t=1      #O(1)
	s=1      #O(1)

	while u<=n:
		for j in range(t): #O(t) 1 + 2 + 3 + 4
			s+=1  #O(1)
		# s+=t
		
		u+=1      #O(1)
		t+=1      #O(1)
	
	return s
```

quante volte si ripete il while?

se n minore di 1 (n=o) allora si ripete 0 volte

se n maggiore di 1:

*esempio:*
n=4
u=1

| Iterazione | valore di n | Operazione | valore di u |
| ---------- | ----------- | ---------- | ----------- |
| 1          | 4           | $u=u+1$    | 2           |
| 2          | 4           | $u=u+1$    | 3           |
| 3          | 4           | $u=u+1$    | 4           |
| 4          | 4           | $u=u+1$    | 5           |

- $u+i = n+1$   oss: $u=1$
- $1+i = n+1$
- $i = n$

Quindi il while si ripete n volte


il for si ripete $t$ volte

**Metodo Monti**

- $\sum\limits^{n}_{u=1}k$

---
**Esercizio 7:**

```python
def es7(n):
	n=abs(n)
	s=n
	t=n
	p=0

	while s >= 1:
		s = s // 4
		p+=1

	while n > 0:
		n-=p
		t+=5

	return t
```

$T(n) = \Theta(\log n) + \Theta\left( \frac{4}{\log n} \right)$

---
**Esercizio 8:**
```python
def es8:
	n=abs(n)
	s=n
	p=2
	i,r=1

	while s >= 1:
		s=s//5
		p+=2

	p=p*p
	while i*i*i < n:
		for j in range(p):
			r+=1
		i+=1
	
	return r
```

costo primo while:
- usciamo dal while quando s=0 ma per comodità scriviamo s=1

- $\frac{s}{5^{i}}=1$ 
- $s=5^{i}$
- $\log s = i\cdot\log{5}$
- $\log_{5}s=i\cdot\log_{5}5$
- $\log s=i$ 

- oss: $s=n$
- Quindi costo primo while è $\Theta(\log n)$


Costo secondo While:
- $p=p\cdot p$ ma $p =2$ quindi $p=2\cdot2=4$
- oss: il costo del for interno al while è costante infatti p è costante (p=4)

- oss: usciamo dal while quando $i^{3} =n$
- $\sqrt[3]{i^{3}}=\sqrt[3]{n}$
- $i = \sqrt[3]{n}$


**Esercizio 9:**



---