---
Created: 2024-04-11
Type: Uni Note
Class:
  - "[[Introduzione agli Algoritmi (class)]]"
Academic Year: 2023/2024
Related: 
Completed: false
---
 ---

>[!info] Index
>1. [[#Introduzione]]
>2. [[#Costi Heap]]
>3. [[#Implementazione]]
>	1. [[#`heapfy()`|heapfy()]]
>	2. [[#`heappop()`|heappop()]]
>	3. [[#`heappush()`|heappush()]]

>[!info] Related
>- [[Heap Sort]]
>- [[Strutture Dati]]
>- [[Introduzione agli Algoritmi (class)]]

---
## Introduzione

La heap è una struttura dati alternativa alla lista che permette di eseguire operazione di inserimento e estrazione in modo più efficiente.

>[!warning] Costi
>
>| Heap |Lista non ordinata | Lista ordinata|
>| --- | --- | --- |
>| Creazione: `θ(n)` | Creazione: `O(1)` | Creazione: `θ(n log n)` |
>| Inserimento: `O(log n)` | Inserimento: `O(1)` | Inserimento: `O(n)` |
>| Estrazione minimo:  `O(log n)` | Estrazione minimo: `θ(n)` | Estrazione minimo: `O(1)` |


>[!tip] Funzioni Python
>Importare Modulo: `from heapq import heapfy, heappush, heappoo`
>- Creazione: `heapfy()`
>- Inserimento: `heappush()`
>- Estrazione minimo:  `heappoo()`

---
## Implementazione 

Un normale array ordinato utilizza un ordinamento orizzontale del tipo `[1, 2 , 5, 9, 11]`, dove passare da un array non ordinato ad uno ordinato ha costo $\Omega(n \cdot \log n)$.

Un Heap utilizza un ordinamento verticale del tipo `[0 ,1 ,3 ,2 ,4 ,5 ,7 ,8 ,9]`, dove passare da un array ad una heap ha un costo $\theta(n)$.

>[!note] Struttura
>![[Pasted image 20240411114928.png|600]]

>[!warning] Rapporto padre figlio
>![[IMG_3048.jpeg|400]]
>
>**oss:** Il valore del nodo padre è sempre più piccolo dei valori nodi dai figli 

---
## Operazioni
Una **Heap** ha 3 operazioni di base:
- [[#Creazione (heapfy)]]
- [[#Estrazione Minimo (heappop)]]
- [[#Inserimento (heappush)]]

---
##### Creazione (heapfy)

>[!info] heapify1
>
>>[!danger] Input
>>1. `A`: Un array di oggetti (su cui sia definito un modo per confrontarli) che verrà trasformato in una Heap.
>>2. `i`: Un indice nell'array. Questo è il nodo che la funzione cercherà di "heapify". In altre parole, la funzione riorganizzerà l'array in modo che il nodo in posizione `i` e tutti i suoi discendenti rispettino la proprietà di heap minimo.
>
>```python
>def heapify1(A, i):
>    # Calcola gli indici dei figli sinistro e destro del nodo i
>    L = 2 * i + 1
>    R = 2 * i + 2
>
>    # Inizializza l'indice del minimo al nodo corrente
>    indice_min = i
>
>    # Se il figlio sinistro esiste e è minore del nodo corrente, aggiorna l'indice del minimo
>    if L < len(A) and A[L] < A[i]:
>        indice_min = L
>
>    # Se il figlio destro esiste e è minore del minimo corrente, aggiorna l'indice del minimo
>    if R < len(A) and A[R] < A[indice_min]:
>        indice_min = R
>
>    # Se il minimo non è il nodo corrente, scambia il nodo corrente con il minimo
>    # e applica ricorsivamente heapify al sottoalbero a partire dal minimo
>    if indice_min != i:
>        A[i], A[indice_min] = A[indice_min], A[i]
>        heapify1(A, indice_min)
>```
>
>>[!warning] Costo Computazionale
>>La funzione `heapify1` ha un **costo temporale** di O(log n) nel caso peggiore. Questo perché, nel caso peggiore, potrebbe dover scendere lungo l'albero fino alla foglia più lontana, che è a una profondità di log n, dove n è il numero di elementi nell'heap.
>>
>>Il **costo spaziale** di `heapify1` è O(1), perché non utilizza spazio di memoria aggiuntivo proporzionale alla dimensione dell'input. La funzione opera "in loco", il che significa che modifica direttamente l'array di input senza creare nuove strutture dati di dimensioni significative. Le uniche variabili che vengono create sono `L`, `R` e `indice_min`, che occupano uno spazio costante indipendentemente dalla dimensione dell'array.
>

>[!info] Heapfy()
>>[!danger] Funzionamento
>>La funzione `Heapify` prende un solo input:
>>1. `H`: Un array di elementi. Questo è l'array che la funzione trasformerà in un heap minimo.
>>
>>La funzione `Heapify` opera "in loco", il che significa che modifica direttamente l'array di input senza creare una nuova copia dell'array.
>>
>>Inizia dal nodo più in basso che ha almeno un figlio (che è `(len(H) - 2) // 2`) e risale fino alla radice dell'heap (che è `0`), chiamando la funzione `heapify1` su ogni nodo per assicurarsi che quel nodo e tutti i suoi discendenti rispettino la proprietà di heap minimo.
>>
>>Come per la funzione `heapify1`, l'array `A` può contenere qualsiasi tipo di elementi, purché sia definito un ordinamento per quegli elementi. In pratica, `H` è spesso un array di numeri.
>
>```python
>def Heapfy(A):
>	
>	for i in range((len(A)-2)//2, -1, -1):
>		heapfy1(A, i)
>```
>
>>[!warning] Costo computazionale
>> - `heapfy1()` ha costo $\Theta(n\log n)$
>> - `heapfy()` si ripete $n$ volte dove $n$ è la lunghezza dell'array
>> 	- a ogni ripetizione la $\sum^{i}_{n=0}$

---
##### Estrazione Minimo (heappop)

```python
def heappop(A):
	x = A[0]
	A[0] = A[len(A) - 1]
	A.pop()
	Heapfy1(A, 0)
	return x
```

>[!warning] Costo computazionale

---
##### Inserimento (heappush)

```python
def Heappush(A, x)
	A.append(x)
	i = len(A) - 1

	while i>0 and A[i] < [(i-1)//2]:
		A[i], A((i-1)//2) = A((i-1)//2), A(i)
		i = (i-1)//2
```

>[!warning] Costo computazionale

---
