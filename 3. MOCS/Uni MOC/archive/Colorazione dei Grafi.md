---
type: Uni Note
class:
  - "[[Algoritmi 1 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-03-07T14:09
updated: 2026-01-31T13:32
---
## Introduzione

Dato un grafo connesso `G`, volgiamo sapere se è possibile colorare in `k` colori diversi i nodi del grafo in modo che nodi addicenti abbiano sempre colori distinti. 

>[!example] Esempio grafo 3-colorabile
>
>![[Pasted image 20250307101133.png|600]]

>[!warning] Minimo e Massimo
>- Il numero massimo di colori è `n` dove `n` è il numero di nodi (grafo completo).
>- Il numero minimo di colori è `1` (caso grafo senza archi).

---
## Algoritmi

Esistono diversi algoritmi che ci permettono di determinare il numero di colori in cui un grafo è colorabile, ad esempio:
- è stato dimostrato che un grafo planare richiede al più 4 colori.
- non si conosce un algoritmo polinomiale per dimostrare che un grafo è 3-colorabile.
- ma si esiste un algoritmo per la [[#Algoritmo bi-colorabile|bi-colorabilità]].

---
## Algoritmo bi-colorabile

Un grafo si dice bi-colorabile se non contiene cicli di numero dispari di nodi.

>[!note] Versione Base
>
>In questo algoritmo se il grafo `G` contiene cicli dispari l’algoritmo produce un assegnamento di colori sbagliato, esiste una [[#^75531e|versione più avanzata]] che ritorna in grafo vettore vuoto quando il grafo non è bi-colorabile.
>
>```python
>def Colora(G):
>	Colore = [-1]*len(G) # vettore di colorati
>	# vettore inizializzato con tutti i nodi non colorati
>	
>	DFSr(0, G, Colore, 0)
>	return Colore
>```
>
>```python
>def DFSr(x, G, Colore, c):
>	'''
>	input: 
>		`x`: nodo da colorare
>		`G`: grafo
>		`Colore`: vettore dei nodi colorati
>		`c`: colore da utilizzare per colorare `x`
>	'''
>	Colore[x] = c
>	for y in G[x]:
>		if Colore[y] ==- 1:         # -1 indica non colorato
>			DFSr(y, G, Colore, 1-c) # colora `y` con l'opposto di `c`

^2a72c3
 
>[!note] Versione Avanzata
>
>Nella versione che segue l’algoritmo produce una bi-colorazione se è bi-colorabile, produce una lista vuota in caso contrario.
>
>Questo viene effettuato colorando il grafo proprio come nella [[#^2a72c3|versione base]], ma viene anche controllato se il nodo che stiamo colorando ha nodi addicenti dello stesso colore (quindi grafo non bi-colorabile), se questo dovesse avvenire un vettore vuoto è tornato come output. 
>
>```python
>def bicolor(G):
>    colori = [0] * len(G) # 0 = non colorato, 1 = rosso, -1 = verde
>    
>    colorabile = DFSr(i, colori, 1, G)
>    
>    if colorabile:
>        return colori
>    else:
>        return []
>```
>
>```python
>def DFSr(x, G, Colore, c):
>	Colore[x] = c
>	for y in G[x]:
>		if Colore[y] == -1:                       # se `y` non è stato ancora colorato
>			Colorabile = DFSr(y, G, Colore, 1-c)  # prova a colore `y`
>			if not Colorabile:                    # se il risultato è non colorabile
>				return false                              
>		elif Colore[x] == Colore[y]:    # controllo se nodi adiacenti di `x` hanno colori uguali
>			return False		
>	return True
>```

^75531e
