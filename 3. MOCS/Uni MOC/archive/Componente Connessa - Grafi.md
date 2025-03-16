---
type: Uni Note
class:
  - "[[Algoritmi 1 (class)]]"
academic year: 2024/2025
related: 
completed: true
created: 2025-03-08T16:20
updated: 2025-03-08T16:20
---
## Componente Connessa

Una ***componente connessa*** di un **grafo indiretto** è un sotto-grafo composto da un insieme massimale di nodi connessi da cammini.

![[Pasted image 20250307141319.png|700]]

>***oss:*** Un *grafo* si dice *connesso* se ha una sola componente connessa.

>[!note] Vettore delle Componenti Connesse
>Le componenti connesse di un grafo possono essere rappresentata in un vettore `C` delle componenti connesse, dove a nodi adiacenti devono avere lo stesso colore e nodi non adiacenti hanno colori diversi.
>
>In particolare il vettore `C` che ha tanti elementi quanti sono i nodi del grafo dove `C[u] = C[v]` se  e solo se i nodi `u` e `v` fanno parte della stessa componente connessa.
>
>![[Pasted image 20250307141729.png|900]]

^867c46

#### Algoritmo

Algoritmo che prende in input un grafo rappresentato attraverso una [[Rappresentazione dei Grafi#Rappresentazione tramite liste di adiacenza|lista di adiacenza]], e ritorna il [[#^867c46|vettore delle componenti connesse]]. ^5d82fa

```python
def Componenti(G)
	'''
	restituisce il vettore `C` delle
	componenti conesse del grafo `G`
	'''

	C = [0]*n    # vettore delle componenti conesse
	c = 0        # colore iniziale
	
	for x in range(len(G)):
		if C[x] == 0:        # se nodo x non ha ancora una componente connessa
			c += 1       
			DFSr(x, G, C, c) # calcola componente di `x`
	return C
```

```python
def DFSr(x, G, C, c):
	C[x] = c
	for y in G[x]:
		if C[y] == 0:
			DFSr(y, G, C, c)
```

>[!example] Esempio
>
>Dato il grafo rappresentato attraverso le lista di adiacenza `G`:
>
>$$
>G = [[1,\, 5],\, [0,\, 5],\, [4],\, [\; ],\, [2],\, [0,\, 1]]
>$$
>
>Otteniamo il vettore delle componenti `C`:
>
>![[Pasted image 20250308122720.png|600]]

>[!danger] Costo
>
>La complessità dalla procedura è $O(n+m)$, dove:
>- `n` deriva dal calcolo di `C = [0]*n`
>- `m` deriva dal resto del codice, che esplora tutti gli archi

---
## Componente Connessa Forte

Una ***componente fortemente connessa*** di un **grafo diretto** è un sotto-grafo composto da un insieme massimale di nodi connessi da cammini.

![[Pasted image 20250308123252.png|500]]

>***nota:*** Un *grafo diretto* si dice **fortemente connesso** se ha *una sola componente*.

### Problema Algoritmo

L'algoritmo visto precedentemente per la [[#Componente Connessa]] non funziona in questa situazione, questo perché non prende in considerazione la direzione degli archi, ad esempio:

Il grafo costituito dalla catena `0 -> 1 -> 2 -> 3 -> 4` se dato in input alla procedura della componente concessa otteniamo `C = [1,1,1,1,1]`, quando in realtà dovremmo ottenere `FC = [1,2,3,4,5]`.

>[!danger] Problema
>
>Il problema risiede nel fatto che se c’è un cammino che da `x` mi porta a `y` questo non significa che `x` e `y` sono nella stessa componente fortemente connessa, perché questo sia vero è necessario che ci sia anche un cammino che da `y` mi porti a `x`.

### Algoritmo componente di un Nodo

>[!done] Soluzioe
>
>Dato il grafo diretto `G` ed un suo nodo `x`, per calcolare i nodi della componente connessa di `x`:
>1. Calcolare l’insieme `A` dei nodi di `G` raggiungibili da `x`.
>2. Calcolare l’insieme `B` dei nodi di `G` che portano a `x`.
>3. Restituire l’intersezione dei due insiemi `A` e `B`.
>
>Per effettuare lo step 2 dobbiamo prima calcolare il grafo trasposto di `G` che chiameremo `GT` e poi ripetere lo step 1 sul grafo trasposto.
>
>>***oss:*** Un **grafo trasposto** è un grafo con gli stessi nodi ma con la direzione di tutti gli archi invertita.
>
>Quindi la nuova procedura sarà:
>4. Calcolare l’insieme `A` dei nodi di `G` raggiungibili da `x`.
>5. Calcolare il grafo `GT` trasposto di `G`.
>6. Calcolare l'insieme `B` dei nodi di `GT` raggiungibili da `x`.
>7. Restituire l’intersezione dei due insiemi `A` e `B`.

>[!danger] Complessità
>
>- Il passo 1 richiede `O(n + m)` (visita DFS che parte da `x` su `G`)
>- Il passo 1 richiede `O(n + m)` 
>- Il passo 1 richiede `O(n + m)` (visita DFS che parte da `x` su `GT`)
>- Il passo 1 richiede `O(n)` 
>
>L'algoritmo avrà dunque come complessità `O(n+m)`.

>[!note] Algoritmo
>
>Prende in input un grafo diretto `G` e un nodo `u` del grafo e ritorna in output un vettore contenente tutti i nodi facente parte della componente di `u`.
>
>```python
>def ComponenteFC(x, G) :
>	visita1 = DFS(x, G)
>	GT = Trasposto(G)
>	vistita2 = DFS(x, GT)
>
>	componente = []
>	for i in range(len(G)):    # oss: len(G) = len(GT)
>		if visitati1[i] == visitati2[i] == 1:
>			componente.append(i)
>	return componente
>```
>
>```python
>def Trasposto(G):
>	n = len(G)
>	GT = [[] for _ in range(n)
>	
>	for i in range(n):
>		for v in G[i]:
>			GT[v].append(i)
>	return GT
>```
>
>Esempio di input e output:
>> ![[Pasted image 20250308160756.png|700]]
>

### Componente connessa di un Grafo

L'algoritmo [[#^5d82fa|appena visto]] `ComponenteFC(x, G)` ci consente di calcolare la componente connessa forte di un solo nodo `x`. Se vogliamo calcolare la componente di tutti i nodi possiamo usare questo algoritmo:

```python
def compFC(G):
	FC = [0]*len(G)
	c = 0
	for i in range(len(G)):
		if FC[i] == 0:
			E = ComponenteFC(i, G)
			c += 1
			for x in E:
				FC[x] = x
	return FC
```

Per ogni nodo del grafo `G` (rappresentato come lista di adiacenza) si determina a quale componente forte appartiene usando la funzione `ComponenteFC(x, G)`.

**Complessità:** $\Theta(n) \cdot O(n+m) = O(n^{2}+nm) = O(n^{3})$ 
