---
Created: 2024-02-26
Type: Uni Note
Class:
  - "[[Introduzione agli Algoritmi (class)]]"
Academic Year: 2023/2024
Related: 
Completed: false
---
---
## Cos'è un algoritmo
**scrivi definizione**
- 

## Esempio costo temporale

```python
def two_pow(n):
	a=1 #C1
	for i in range(n): #costo variabile, dipende da n
		a = a*2 #C2
	print(a) #C3
```

**Esistono 2 tipi di costati:**
- Costanti additive e moltiplicative

- Costo programma = $C1 + C2\cdot n + C_{3}$
	- C1 e C3 sono sostanti additive
	- C2 + una costante moltiplicativa

### Notazioni
- **Upper Bound:** $O(n)$

- **Lower Bound:** $\Omega(n)$

- **Costo asintotico:** $\Theta(n)$

$f(n)\in O(n)$ --> $f(n)$ appartiene all'insieme delle funzioni che crescono in modo lineare

$$
f(n)=O(\exists c>0,\ n\geq 0\ \  t.c.\ f(n)\leq cg(n)\ \ \forall n\geq n_{0})
$$

**oss:** gli algoritmi sono sempre funzioni asintotiche positive



**Dimostrare che:**
- $f(n)=a\cdot n^{2}+b = O(n^{2})$

*Procedimento:* $an^{2}+b\ \ \leq \ \ an^{2} + |b|\ \ \leq \ \ an^{2} + b\cdot n^{2}$ 
- oss: $an^{2} + \cdot n^{2} = (a+ |b|) n^{2}$ --> $a+|b| = c>0$
- Quindi: $f(n) = cn^{2}\ \ \ \forall n\geq 1$

