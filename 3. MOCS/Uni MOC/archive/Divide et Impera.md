---
created: 2024-04-25
type: Uni Note
class:
  - "[[Algoritmi 1 (class)]]"
  - "[[Algoritmi 2 (class)]]"
academic year: 2023/2024
related:
completed: true
updated: 2026-01-31T13:32
---
## Definizione

Il paradigma **divide et impera** anche conosciuto come **divide and conquer** consiste nella creazione di algoritmi che *dividono il problema principale in sotto problemi di difficolta inferiore*.

In particolare è possibile trovare *tre fasi*:

>[!note] Fase 1 (divide)
>
>La prima fase consiste nel dividere un problema dato in istanze o sottoproblemi più piccoli. Questo è ripetuto anche per i sotto problemi che verranno ulteriormente divisi in sottoproblemi più piccoli fino a raggiungere una fase in cui non sono più possibili ulteriori divisioni.

>[!note] Fase 2 (impera)
>
>La seconda fase consiste nel risolvere i sottoproblemi generati nella prima fase. Questa comporta la risoluzione di molti sottoproblemi in modo ricorsivo. 
>
>Tuttavia, a volte non è necessario risolvere i sottoproblemi poiché sono già segnati come risolti di per sé dopo la fase di divisione, vedi [[Programmazione Dinamica]].

>[!note] Fase 3 (combina)
>
>La fase finale consiste nel combinare ricorsivamente le soluzioni dei sottoproblemi fino a raggiungere uno stadio in cui si ottiene una soluzione al problema originale.

---
## Esempio (problema della selezione)

Data una lista `A` di `n` interi distinti, ed un intero `k`, con $1 \leq k \leq n$, vogliamo sapere quale elemento occuperebbe la posizione `k` se il vettore venisse ordinato.

Individuiamo alcuni casi particolari:

- Per $k=1$ abbiamo il minimo di `A`
- Per $k=n$ avremo il massimo di `A`
- Per $k= \left\lceil  \frac{n}{2}  \right\rceil$ avremo il mediano di `A`

#### Soluzione Base

Una semplice soluzione con complessità $\Theta(n \log n)$ è:

```python
def sol1(A, k):
	A.sort()
	return A[k-1]
```

Vedremo che utilizzando un algoritmo che si basa sul paradigms divide et impera è possibile risolvere questo problema in $\Theta(n)$.

***Approccio basato sul divide et Impera:***
1. Scegliere nella lista `A` l’elemento in posizione `A[0]` che chiameremo **perno**.
2. Partendo dalla lista `A` costruiamo due liste `A1`​e `A2​`, la *prima* contiene gli elementi di `A` *minori* del perno e la *seconda* i *maggiori*.

Dove si trova l’elemento di *rango* `k`, ci sono tre casi:
1. Se $|A_{1}​| \geq k$ allora l’elemento di rango `k` è nel vettore `A1`.​
2. Se $|A_{1}​| = k−1$ allora l’elemento di rango `k` è proprio il *perno*.
3. Se $|A_{1}​| < k−1$ allora l’elemento di rango `k` è in `A2`​, è l’elemento di rango `k−|A1​|−1` in `A2​`.

Quindi soltanto nel secondo casa abbiamo una risposta definitiva:
1. Nel *caso 1* dobbiamo richiamare l'algoritmo sulla lista `A1` invece che `A`.
2. Nel *caso 2* dobbiamo richiamare l'algoritmo sulla lista `A2` inviteece che `A` ed in particolare il rango non sarà più `k` ma `k−|A1​|−1`.

```python
def selezione2(A,k):
	if len(A) == 1: return A[0]
	
	perno = A[0]
	A1, A2 = [], []
	
	for i in range(len(A)):
		if A[i] < perno:
			A1.append(A[i])
		else:
			A2.append(A[i])
	
	if len(A1) >= k:
		return selezione2(A1, k)
	elif len(A1) == k-1:
		return perno
	
	return selezione2(A2, k - len(A1) - 1)
```

>[!danger] Costo Computazionale Caso Peggiore
>
>Questa procedura che tripartisce la lista può però restituire una partizione massimamente sbilanciata in cui si ha ad esempio $|A1| = 0$, |$A2| = n−1$, questo accade quando il perno risulta l'elemento minimo nella lista.
>
>
>Nel caso in cui questo evento sfortunato si ripete ad ogni partizione creata dall’algoritmo allora la complessità dell'algoritmo al caso pessimo è descritta da:
>$$
>T(n) = T(n-1) + \Theta(n)
>$$
>il cui risultato è
>
>$$
>T(n) = \Theta(n^{2})
>$$

>[!danger] Costo Computazionale Generale
>
>Più in generale il costo di questo algoritmo è rappresentato dalla seguente funzione:
>
>$$
>T(n) = T(m) + \Theta(n)
>$$
>
>Dove `m` è $\max\{ |A_{1}|,\, |A_{2}| \}$.
>
>Quindi se venisse sempre scelto un perno che garantisca un equilibrio fra le liste che crea l’algoritmo avremo che:
>
>$$
>m = max\{ |A_{1}|, \, |A_{2}| \} \approx n/2
>$$
>
>allora la complessità `T(n)` dell'algoritmo sarebbe:
>
>$$
>T(n) = T\left( \frac{n}{2} \right) = + \Theta(n) = \Theta(n)
>$$
>
>Naturalmente aspettarsi che il perno venga scelto sempre in una posizione tale da rendere le liste perfettamente bilanciate è irrealistico, potremmo allora accontentarci di chiedere che la scelta del perno garantisca partizioni non troppo sbilanciate come ad esempio quelle per cui:
>
>$$
>m = \max \{  |A_{1}|, \, |A_{2}| \} \approx 3n/4
>$$
>
>In questo caso si ha che:
>
>$$
>T(n) \leq T\left( \frac{3}{4}n \right) + \Theta (n)
>$$
>
>Che risulta ancora $T(n)= \Theta(n)$

#### Soluzione Probabilistica

Proviamo quindi a scegliere il perno a caso in modo equiprobabile tra gli elementi della lista, in questo modo anche se la scelta non produce una lista perfettamente bilanciata avremo comunque una complessità lineare.

```python
def selezione2R(A, k):
 
	if len(A)==1: return A[0]
		
	perno = A[randint(0, len(A) - 1)]
	A1, A2 = [], []
	
	for x in A:
		if x < perno:
			A1.append(x)
		elif x > perno:
			A2.append(x)
	
	if len(A1) >= k:
		return selezione2R(A1, k)
	elif len(A1) == k - 1:
		return perno
	
	return selezione2R(A2, k - len(A1) - 1)
```

Con questo algoritmo abbiamo che con alta probabilità il costo è lineare mentre al caso peggiore, che accade con una probabilità molto piccola è di $O(n^{2})$. Per questo si dice che il costo medio è lineare.

>[!warning]- Dimostrazione
>
>![[Pasted image 20250427163913.png]]
>
>![[Pasted image 20250427163932.png]]
>
>![[Pasted image 20250427164009.png]]

#### Soluzione Deterministica

Per questo problema esiste una soluzione deterministico che garantisce una complessità $\Theta(n)$ anche per il caso pessimo.

Questo modo noto come **mediano dei mediani**, garantisce che il perno scelto produce sempre due sotto liste `A1` e `A2`, ciascuna delle quali ha non più di ​$\frac{4}{3}n$ elementi.

L'algoritmo è basato sul paradigma divide et impera e segue questi passi:
- Divide l’insieme `A`, contenente `n` elementi, in gruppi da 5 elementi ciascuno. L’ultimo gruppo potrebbe avere meno di 5 elementi.
- Trova il mediano all’interno di ciascuno di questi $\left\lfloor  \frac{n}{5}  \right\rfloor$ gruppi.
- Calcola il mediano `p` dei mediani ottenuti al passo precedente.
- Usa `p` come elemento pivot per l’insieme `A`.

>[!example] Esempio 
>
>$$
>A = [15, 2, 10, 16, 21,12, 1, 9, 11, 17, 22, 3, 8,13, 14, 4, 9, 19, 5, 6, 20, 23,18, 7]
>$$
>
>**1)** Si divide l'insieme in gruppi da 5 elementi (tranne ultimo):
>- $G_{1} = 15, 2, 10, 16, 21$
>- $G_{2} = 12, 1, 9, 11, 17$
>- $G_{3} = 22, 3, 8, 13, 14$
>- $G_{4} = 4, 19, 5, 6, 20$
>- $G_{5} = 23, 18, 7$
>
>**2)** Troviamo il mediano (si ordinano le sotto liste e si sceglie l'elemento centrale):
>- $G_{1} = 2,10, \textcolor{orange}{15}, 16, 21$
>- $G_{2} = 1, 9, \textcolor{orange}{11},12, 17$
>- $G_{3} = 3, 8, \textcolor{orange}{13}, 14, 22$
>- $G_{4} = 4, 5, \textcolor{orange}{6}, 19, 20$
>
>**3)** si calcola il mediano dei mediani, ripetendo ricorsivamente l'algoritmo, in questo caso essendo soltanto `4` mediani abbiamo un solo gruppo di `4` elementi:
>- $G = 15, 11, 13, 6$, una volta ordinato $G = 6, \textcolor{orange}{11}, 13, 15$
>  
>Quindi il perno è l'elemento `11`

```python
def selezione(A, k):
	if len(A) <= 120:
		A.sort()
		return A[k - 1]
	
	B = [sorted(A[5*i:5*i+5])[2] for i in range(len(A)//5)]
	perno = selezione(B, ceil(len(A)/10))
	A1, A2 = [], []
	
	for x in A:
		if x < perno:
			A1.append()
		elif x > perno:
			A2.append()
	
	if len(A1) >= k:
		return selezione(A1, k)
	elif len(A1) == k - 1:
		return perno
	
	return selezione(A2, k - len(A1) - 1)
```

Questo algoritmo quindi risolve il problema in modo lineare anche al caso pessimo, però a causa delle grandi costanti nascoste nell’$O(n)$, in realtà l’algoritmo probabilistico visto precedentemente si comporta meglio.

