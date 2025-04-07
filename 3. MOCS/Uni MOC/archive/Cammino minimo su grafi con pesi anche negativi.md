---
type: Uni Note
class: "[[Algoritmi 2 (class)]]"
academic year: 2024/2025
related: 
completed: true
created: 2025-04-07T10:07
updated: 2025-04-07T10:07
---
## Introduzione

Per effettuare una ricerca dei cammini minimi in un grafo con pesi negativi dobbiamo assicuraci che non esistano cicli con peso totale negativo all interno del grafo.

>[!note] Ciclo Negativo
>
>Un ciclo negativo è un ciclo diretto in un grafo in cui la somma dei pesi degli archi che lo compongono è negativa.
>
>![[Pasted image 20250405202646.png|500]]
>
>Il ciclo in figura ha costo: `5-3-6+3-2 = -2`

>[!danger] Problema
>
>Se in un cammino tra i nodi `s` e `t` è presente un nodo appartiene ad un ciclo negativo, allora non esiste il cammino di costo minimo tra `s` e `t`.
>
>![[Pasted image 20250405202944.png|550]]
>
>Questo perché per il ciclo `W` si ha `costo(W) < 0`, ripassando più volte attraverso il ciclo `W` possiamo abbassare arbitrariamente il costo del cammino da `s` a `t`.

>[!warning] Proprietà
>
>Se il grafo `G` non contiene cicli negativi, allora per ogni nodo `t` raggiungibile dalla sorgente `s` esiste un cammino di costo minimo che attraversa al più `n-1` archi.
>
>Questo perché un cammino minimo non percorre mai un nodo più di una volta.
>
>***Quindi:*** Questo garantisce che il costo minimo può essere calcolato considerando solo cammini di questa lunghezza.

## # Algoritmo di Bellman - Ford

Se il grafo `G` non contiene cicli negativi, allora per ogni nodo `t` raggiungibile dalla sorgente `s` esiste un cammino di costo minimo che attraversa al più `n - 1` archi.

Per l’algoritmo definiamo quindi la seguente tabella `T` di dimensione `n x n` dove:
- `T[i][j]` = costo di un cammino minimo da `s` al nodo `j` di lunghezza al più `i`.

In particolare la prima riga avrà tutti $-\infty$ ad eccezione della sorgente cha ha valore `0`.

Per calcolare i valori delle altre righe dobbiamo distinguere due casi:

>***Caso 1:***
>
>Se il costo per raggiungere `j` ha **lunghezza inferiore o uguale** al valore `i` allora *prendiamo il valore precedente della tabella*, quindi `T[i][j] = T[i][j - 1]`.

>***Caso 2:***
>
>Se *caso 1* è falso allora deve esistere un cammino minimo di lunghezza più `i - 1` ad un nodo `x` il quale poi tramite un arco ci porterà a `j`. 
>
>Dobbiamo quindi prendere il cammino minimo fra tutti questi cammini che ci portano dalla sorgente ad un `x` e da `x` a `j` tramite un solo arco, ovvero:
>
>$$
>T[i][j] = min_{(x-1)\in E}(T[i][j] + T[i][j-1])
>$$

Ovviamente non sappiamo in quale dei due casi ci troviamo e quindi prendiamo il minore fra questi due casi:

$$
T[i][j] = min(T[i][j]=T[i][j−1],min_{(x−1)\in E}​(T[i−1][x]+costo(x,j)))
$$

La soluzione al nostro problema sarà all'ultima riga.

## Calcolo Costo Cammini Minimi

Implementiamo un algoritmo per il calcolo il costo del cammini minimi, che calcola il costo del cammino minimo che parte da un nodo `s` e raggiunge ogni nodo del grafo.

```python
def CostoCammini(G, s):
	n = len(G)
	
	T = [[float('inf')] * n for _ in range(n)]
	T[0][s] = 0
	
	GT = Trasposto(G)
	for i in range(1, n):
		for j in range(n):
			T[i][j] = T[i - 1][j]
			if j != s:
				for x, costo in GT[j]:
					T[i][j] = min(T[i][j], T[i-1][x] + costo)
	return T[n-1]
 
def Trasposto(G):
	
	GT = [[] for _ in G]
	for i in range(len(G)):
		for j, costo in G[i]:
			GT[j].append((i, costo))

	return GT
```

Per migliorare l'efficenza e per conoscere gli archi entranti al nodo `j`, conviene calcolare il grafo trasposto `GT` di `G`, in questo modo in `GT[j]` avremo tutti i nodi `x` tali che in `G` esiste l’arco `x -> j`.

>[!danger] Costo
>- La tabella costa $\Theta(n^{2})$.
>- Calcolare il trasposto $O(n+m)$
>- I due `for` più interni in realtà scorrono le liste di adiacenza dei nodi quindi hanno un costo totale di $\Theta(m)$ mentre quello esterno $\Theta(n)$. In totale i 3 for costano $\Theta(n\cdot m)$
>
>Quindi il costo totale è di $O(n^{2}+nm)$

## Calcolo Cammini Minimi

Precedentemente abbiamo calcolato il costo per raggiungere i nodi ora ci interessa trovare anche i nodi da percorrere per effettuare qui cammini, dobbiamo quindi modificare l’algoritmo in modo che ci restituisca il vettore dei padri.

Per fare ciò dobbiamo mantenere per ogni nodo `j` il suo predecessore `P[j]`, questo valor andrà aggiornato ogni volta che il valore `T[k][j]` cambia, ovvero quanto un nuovo  percorso minore è stato trovato.

```python
def CostoCammini(G, s):
	n = len(G)

	T = [[float('inf')] * n for _ in range(n)]
	T[0][s] = 0
	
	P = [-1] * n
	P[s] = s
	
	GT = Trasposto(G)
	for k in range(1, n):
		for j in range(n):
			if j == s:
				T[k][j] = 0
			else:
				for x, costo in GT[j]:
					if T[k-1][x] + costo < T[k][j]:
						T[k][j]=T[j-1][x] + costo
						P[i] = x
	return T[n-1], P
```

>[!warning] Ottimizzazioni
>
>**Proprietà Tabella:**
>- Se notiamo che una riga è uguale alla precedente allora anche le righe successive non cambieranno, possiamo quindi terminare l’algoritmo.
>- Non serve avere sempre in memoria l’intera tabella, ci basta l’ultima riga e la precedente. In questo modo riduciamo la complessità di spazio da $O(n^{2})$ a $O(n)$.
>  
>**Rilevamento Cicli Negativi:**
>- Questo algoritmo non si accorge se ci sono o no cicli negativi, se vogliamo però effettuare un test, ci basta calcolare i percorsi fino a distanza `n`, aggiungendo quindi una riga.
>- Le ultime due righe `n−1` e `n` saranno uguali se e solo se nel grafo non ci sono cicli negativi raggiungibili da `s`. Implementare il test non cambia l’asintotica dell’algoritmo.