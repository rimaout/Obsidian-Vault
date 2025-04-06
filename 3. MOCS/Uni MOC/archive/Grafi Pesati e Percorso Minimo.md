---
type: Uni Note
class: "[[Algoritmi 2 (class)]]"
academic year: 2024/2025
related: 
completed: true
created: 2025-04-05T17:29
updated: 2025-04-05T20:20
---
## Introduzione

Un Grafo pesato è un grafo i cui archi hanno un peso (valore), solitamente più questo valore è alto più è svantaggioso percorrere un determinato arco.

>[!note] Rappresentazione Grafo Pesato
>
>Per rappresentare un grafo pesato possiamo sempre utilizzare una un vettore di liste di adiacenza deve le liste di adiacenza contengono tuple il cui primo elemento è il nodo da raggiungere ed il secondo elemento è il peso dell'arco.
>
>Quindi per rappresentare l'arco `(x,y)` con peso `c`, nella lista di adiacenza di `x` i sarà la coppia `(y, c)`, ad esempio:
>
>```python
>G = [
>	[(1, 17), (5, 4)],
>	[(0, 17), (4, 5),  (5, 6)],
>	[(3, 12), (4, 10)],
>	[(2, 12), (4, 4),  (5, 1)],
>	[(1, 5),  (2, 10), (3, 4)],
>	[(0, 4),  (1, 6),  (3, 1)]
>]
>```

Se vogliamo trovare il **percorso minimo** (con peso minimo) per andare da un nodo `x` ad un nodo `y` possiamo usare due tecniche diverse [[#Suddivisione degli Archi]] e [[#Algoritmo di Dijkstra]].

## Suddivisione degli Archi

Consiste nell'inserire dei **nodi dummy** negli archi, ad esempio se tra due nodi addicenti `x` e `y` sono uniti da un arco di peso 3 inseriamo due nodi finti in modo che è come se attraversassimo 3 archi invece che 1:

![[Pasted image 20250324100717.png|500]]

Ora per trovare il percorso minimo possiamo utilizzare una [[Visita in Ampiezza (BFS) - Grafi|visita BFS]] a partire dal nodo `x` e che si ferma appena trovato il nodo `y`.

>[!danger] Costi
>
>Effettuare questa visita avrà costo $O(n'+m')$ dove `n'` e `m'` sono rispettivamente il numero nodi e di archi del grafo avente i *nodi dummy*.
>
>Il costo di questa soluzione dipende strettamente al peso di nodi, quindi è consigliato utilizzarla soltanto quando i **pesi** degli archi sono **interi** e abbastanza **piccoli**.

## Algoritmo di Dijkstra

Algoritmo di Dijkstra permette di trovare l'albero dei cammini minimi lavorando direttamente su grafi pesati (con pesi anche non interi).

Si basa sul **paradigma della tecnica greedy**, ovvero si effettua la scelta ottimale a livello locale ad ogni passo nella speranza di trovare una soluzione ottimale globale.

>[!note] Funzionamento ad alto livello
>
>L'obbiettivo è costruire l’albero dei cammini minimi un arco per volta partendo dal nodo sorgente, dove:
>- Ad ogni passo aggiungi all’albero l’arco che produce il nuovo cammino più economico.
>- Alla nuova destinazione assegna come distanza il costo del cammino.
>  
>![[Screenshot 2025-03-23 at 16.51.27.png|800]]

### Versione Ottimale per Grafi Densi

**Idea:** creiamo un vettore dove per ogni nodo `x` del grafo memorizza una terna `(definitivo, costo, origine)`, dove:

>***Definitivo*** è una flag che indica che può assumere due valore:
>- `1` se il costo per raggiungere il nodo `x` è stato stabilito definitivamente, ovvero  se l’algoritmo ha confermato che non è possibile ottenere un percorso migliore a partire dalla sorgente.
>- `0` se il costo per raggiungere il nodo `x` è ancora in fase di aggiornamento (non definitivo).

>***Costo:*** 
>- Rappresenta il costo corrente minimo noto per raggiungere `x` dalla sorgente `s`.
>- All’inizio, per ogni nodo diverso da `s` questo valore è inizializzato a $+\infty$, e per `s` a `0`. 

>***Origine:*** 
>- Indica il nodo ”padre” o ”predecessore” lungo il cammino minimo dalla sorgente `s` a `x`.
>- Se non è ancora stato trovato un percorso per `x` oppure `x` non ha ancora un predecessore, questo valore è inizialmente impostato a `-1`.

>[!note] Codice
>
>```python
>def dijkstra(s, G):
>	'''
>	Restituisce il vettore delle distanze D e l'albero dei cammini 
>	minimi rappresentato attraverso il vettore dei padri 
>	'''
>	n = len(G)
>	
>	# Inizializzazione Lista: `definitivo` = 0, `costo` = infinito, `origine` = -1
>	Lista = [(0, float('inf'), -1)] * n
>		
>	# Impostiamo il nodo sorgente
>	Lista[s] = (1, 0, s)
>
>	# Aggiorno i vicini di `s` (non sono definitivi)
>	for y, costo_arco in G[s]:
>		Lista[y] =(0, costo_arco, s)
>	
>	while True:
>		
>		# Cerco nodo non definitivo con costo minimo
>		minimo, x = float('inf'), -1
>		for i in range(n):
>			if Lista[i][0] = 0 and Lista[i][1] < minimo:
>				minimo, x = Lista[i][1], i
>
>		if minimo == float('inf'):
>			# non ci sono più nodi raggiungibili non definiti
>			break
>			
>		# Rendiamo definitivo il nodo `x`
>		definitivo, costo_x, origine = Lista[x]
>		Lista[x] = (1, costo_x, origine)
>		
>		# Aggiorniamo eventualmente i vicini di `x` non definitivi
>		for y, costo_arco in G[x]:
>			# `y` non è definitivo e passando per `x` c'è un cammino migliore
>			if Lista[y][0] == 0 and minimo + costo_arco < Lista[y][1]:
>				Lista[y] = (0, minimo + costo_arco, x)
>	
>	# Estraiamo dalla lista il vettore delle distanze e dei padri
>	D, P = [costo for _, costo, _ in Lista], [origine for _, _, origine in Lista]
>	return D, P
>```
>
>![[Pasted image 20250324094529.png|600]]

>[!danger] Costo
>
>- Il costo delle istruzioni al di fuori del while è $\Theta(n)$.
>- Il while viene eseguito al più `n-1` volte (ad ogni iterazione un nuovo nodo viene selezionato e reso definitivo). All’interno del while c'è:
>	- il primo `for` che viene iterato esattamente `n` volte
>	- il primo `for` che viene eseguito al più `n` volte (tante volte quanti sono gli adiacenti presenti nella lista del nodo appena inserito nell’albero).
>
>Il costo del while è dunque $\Theta(n^{2})$ e questa è anche la complessità dell’implementazione.
>
>>***oss:*** Questa implementazione è considerabile **ottima** nel caso di grafi sensi dove $m = \Theta(n^{2})$.

### Versione Ottimale per Grafi Sparsi

Sostituendo il vettore lista con un *heap minimo* potremmo estrarre l’elemento minimo in tempo logaritmico nel numero di elementi presenti nell’heap, **idea**:
- Manteniamo una *heap minimo* contenente triple `(costo, u, v)` dove `u` e un nodo già inserito nell’albero dei cammini minimi e costo rappresenta la distanza che si avrebbe qualora il nodo y venisse inserito nell’albero dei cammini minimi attraverso il nodo x.

```python
from heapq import heappush, heappop

def dijkstra1(s, G):
	'''
	Restituisce il vettore delle distanze e
	l'albero dei cammini minimi tramite il vettore dei padri
	'''
 
    n = len(G)
    D = [float('inf')] * n  # Distanze inizialmente infinite
    P = [-1] * n  # Predecessori inizializzati a -1
    
    # la sorgente dista 0 da se stessa
    D[s] = 0
    
    # La sorgente è la radice dell'albero delle distanze
    P[s] = s
    H = []  # Min-heap
    
    # Inizializziamo l'heap con i vicini della sorgente
    for y, costo in G[s]:
        heappush(H, (costo, s, y))  # (costo, x=s, y)
    
    while H:
        # Estrai il nodo con distanza minore
        costo, x, y = heappop(H)
        if P[y] == -1:
            # inserisci y nel vettore dei padri come figlio di x
            P[y] = x
            # setta la distanza minima di y
            D[y] = costo
            for v, peso in G[y]:
                # Esplora i vicini di y
                if P[v] == -1:
                    # Se v non è ancora stato aggiunto all'albero
                    heappush(H, (D[y] + peso, y, v))
    
    # Restituisce le distanze e i predecessori
    return D, P
```

>[!danger] Costo
>
>Nota che nell’heap `H` possono esserci anche $O(m)$ elementi e quindi i costi di inserimento ed estrazione saranno $O(\log m) = O(\log n^{2}) = O(\log n)$.
>
>**Complessità dell'implementazione:**
>
>>***Inizializzazione*** - prima dell’accesso al while abbiamo l’inizializzazione di:
>>- `D` e `P` per un costo $\Theta(n)$ 
>>- L’inserimento dei vicini di `s` nell’heap per un costo di $O(n \log n)$.
>
>>***While (iterazioni)*** - il numero di iterazioni del while è $\Theta(n)$, infatti:
>>- ad ogni iterazione del `while` si elimina un elemento da `H` e eventualmente per mezzo del `for` annidato si scorre la lista di adiacenza di un nodo e vengono aggiunti elementi ad `H`.
>
>>***While (costo)*** - il costo totale del `while`, senza tener conto del `for`, è $O(m \log m)$, infatti:
>>- Il costo di ciascuna iterazione del while richiede O(log n) a causa dell’estrazione da `H`
>
>>***For*** - il tempo totale richiesto dalle varie iterazioni del `for` annidato nel while è $O(m \log n)$ in quando ad ogni iterazione scorro una lista di adiacenza diversa. 
>>
>>In totale scorrerò $O(m)$ archi e per ogni arco pagherò $O(\log n)$ per inserimento in `H`.
>
>La complessità di questa implementazione è dunque:
>
>$$
>O(n \log n) + O(m \log n) + O(m \log n) = O((n+m)\log n)
>$$