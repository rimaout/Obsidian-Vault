---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-03-20T16:15
updated: 2025-03-24T15:06
---
# Albero minimo di copertura

## Introduzione

L'albero minimo di copertura è un albero che collega tutti i nodi di un grafo con il minor costo possibile, dove costo si intende la somma del peso di tutti i nodi.

![[Pasted image 20250324101059.png|400]]

Nel mondo reale sarebbe come creare una rete ferroviaria che collega tutte le stazioni usando il minor numero possibile di kilometri di ferrovie, questo non assicura che si colleghino le stazioni con i percorsi più brevi, ma ci permette di risparmiare sulle ferrovie utilizzate.

>[!warning] Osservazioni
>
>- Potrebbe contenere cammini non minimi.
>- Albero dei cammini minimi assicura che tutti i nodi siano connessi con i percorsi con il costo più basso, invece l'albero di copertura minima assicura che tutti i nodi sono connessi tra di lore e che questo venga fatto con il minor costo possibile.
>- L'albero è un grafo aciclico, se ci fosse un ciclo significherebbe che si potrebbe ridurre il costo rimuovendo un arco superfluo.

## Algoritmo di Kruskal

- Partendo dal grafo in input `G` creiamo un grafo `T` che contiene tutti i nodi di `G` ma nessun arco.
- Partendo da un nodo iniziale percorriamo gli archi del grafo `G` creando un percorso di costo crescente.
- Ad ogni iterazione controlliamo se è possibile aggiungere a `T` l'arco che stiamo analizzando senza creare un ciclo.
- Se il nuovo arco non crea un ciclo allora lo inseriamo in `T`.
  
L’algoritmo rientra perfettamente nel paradigma della **tecnica greedy**:
- La sequenza di decisioni irrevocabili: decidi per ciascun arco di G se inserirlo o meno in T. Una volta deciso cosa fare dell’arco non ritornare più su questa decisione.
- Le decisioni vengono prese in base ad un criterio “locale”: se l’arco crea ciclo non lo prendi, in caso contrario lo prendi in quanto è il meno costoso a non creare cicli tra gli archi che restano da considerare.  

![[Pasted image 20250324110058.png|600]]

### Implementazione non Ottimizzata

```python
def kruskal(G):
	# Creare una lista con gli archi pesati di `G`
	E = [(c, u, v) for u in range(len(G)) for v,c in G[u] if u<v]

	# Ordinare gli archi in ordine crescente di peso
	E.sort()
	
	# Per ogni arco, inseriamolo nel grafo se non crea un ciclo 
	T = [[] for _ in G]
	for c, u, v in E:
		if not conessi(u, v, T):
			T[u].append(v)
			T[v].append(u)
	return T	
```


>[!danger] Costo
>L'ordinamento costa $O(m \log m)$ che nel caso peggiore è $O(m \log n^{2}) = O(m \log n)$.
>
>Il `for` è ripetuto `m` volte e determinare se i due nodi `u` e `v` sono connessi (funzione connessi) ha costo $O(n)$, portando il costo totale del `for` a $O(n\cdot m)$
>
>Quindi il *costo totale* è $O(m \log n) + O(m\cdot n) = \textcolor{orange}{O(m\cdot n)}$

## UNION-FIND

Il costo elevato della [[#Implementazione non Ottimizzata|versione appena vista]] dipende fatto che utilizziamo la funzione connessi per determinare se due nodi sono uniti da un percorso.

Per ridurre questo costo utilizziamo la struttura dati UNION-FIND per determinare efficientemente se i due nodi appartengono alla stessa componente connessa.

>[!note] Definizione
>
>La UNION-FIND è una struttura dati utilizzata per rappresentare una collezione `C` di componenti connesse, permette di effettuare le due seguenti operazioni:
>- `Union(A,B,C)` modifica la struttura dati `C` fondendo la componente `A` alla componente `B` e ritorna il "nome" della nuova componente connessa, in **tempo** $O(1)$.
>- `Find(x, C)` restituisce il nome della componente connessa in `C` contente il nodo `x`, in **tempo** $O(\log n)$.
>- `Create(HG)` restituisce la struttura dati Union-Find generata partendo da un grafo, in **tempo** $\Theta(n)$ .

>[!note] Funzione Crea
>
>Funzione che partendo da un grafo `G` crea la struttura dati Union-Find ovvero un vettore `C`.
>
>La funzione genera un albero per ogni componente connessa, ogni elemento del vettore `C` in posizione `i` rappresenta il padre che il nodo `i` del grafo ha nel albero della sua componete connessa.
>
>>***oss:*** `C` può essere visto come un vettore dei padri.
>
>***METTI IMMAGINE***
>
>```python
>def Crea(G):
>	C = [ (i, p) for i in range(len(G))]
>	return C
>```

>[!note] Funzione Find
>
>Funzione che data un nodo `x` e una Union-Find  `C` ritorna il "nome" della componente connessa a cui `x` appartiene.
>
>Per nome della componente connessa si intende il nodo radice del albero che rappresenta la componente connessa di `x`.
>
>Per trovare questa radice ci bassa "inseguire" i padri in `C` (C può essere visto come un vettore dei padri) fino a quando troviamo un nodo che ha come padre se stesso.
>
>```python
>def Find(u, C):
>	while u != C[u]:
>		u = C[u]
>	return u
>```

>[!note] Funzione Union
>
>```python
>def Union(a, b ,C)
>	tota, totb = C[a][1], C[b][1]
>	
>	if tota >= totb:
>		C[a] = (a, tota + totb)
>		C[b] = (a, totb)
>	else:
>		C[a] = (b, tota)
>		C[b] = (b, tota + totb)
>```