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

---
## Introduzione

La heap è una struttura dati alternativa alla lista che permette di eseguire operazione di inserimento e estrazione in modo più efficiente rispetto a una lista.

>[!tip] Funzioni Python
>Importare Modulo: `from heapq import heapfy, heappush, heappoo`
>- Creazione: `heapfy()`
>- Inserimento: `heappush()`
>- Estrazione minimo:  `heappoo()`

---
## Costi Heap
- Creazione: `O(n)`
- Inserimento: `O(log n)`
- Estrazione minimo:  `O(log n)`

>[!warning] Costi Lista
>
>| Lista non ordinata | Lista ordinata crescente | Lista ordinata decrescente |
>| --- | --- | --- |
>| Creazione: `O(1)` | Creazione: `O(n log n)` | Creazione: `O(m log n)` |
>| Inserimento: `O(1)` | Inserimento: `O(n)` | Inserimento: `O(n)` |
>| Estrazione minimo: `O(n)` | Estrazione minimo: `O(n)` | Estrazione minimo: `O(1)` |
>**oss:** Inserimento deve mantenere l'ordinamento

---
## Implementazione 

Un normale array ordinato utilizza un ordinamento orizzontale del tipo `[1, 2 , 5, 9, 11]`, dove passare da un array non ordinato ad uno ordinato ha costo $\Omega(n \cdot \log n)$.

Un Heap utilizza un ordinamento verticale del tipo `[0 ,1 ,3 ,2 ,4 ,5 ,7 ,8 ,9]`, dove passare da un array ad una heap ha un costo $\theta(n)$.

>[!note] Struttura
>![[Pasted image 20240411114928.png|600]]

>[!warning] Rapporto padre figlio
>![[IMG_3048.jpeg|400]]

##### `heapfy()`


##### `heappop()`

```python
def heappop(A):
	x = A[0]
	
```

##### `heappush()`

---
