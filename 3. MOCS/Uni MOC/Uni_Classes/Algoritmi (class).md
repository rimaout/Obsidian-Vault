---
Academic Year: 2023/2024
Type: Uni Note
Link: https://twiki.di.uniroma1.it/twiki/view/Intro_algo/PZ/WebHome
---
---
**Lezioni:**
1. [[AL 26 Feb]]
2. [[AL 29 Feb]]
3. [[Al 07 Mar]]
4. [[Al 11 Mar]]
5. [[Al 14 Mar]]

**Argomenti:**
- [[Concetti di base x Algoritmi]]
- [[Notazione asintotica per calcolo costo computazionale]]
- [[Algoritmi di ricerca]]

- [[Algoritmi]], [[Algoritmi Iterativi]], [[Algoritmi Ricorsivi]]

```python
def SommaLista(L, i=0):
	if len(L)-i == 0:
			return 0
	else:
		return Sommalista(L, ++i) + L[len(i)-i]
```

$$
T(n) = \begin{cases}
\Theta(1) &\text{if } n-i=0 \\
T(n-1)+\Theta(1)
\end{cases}
$$

---
```python
def MinList(L, i=0)
if len(L)==1:
	return L[0]
	
	
```
