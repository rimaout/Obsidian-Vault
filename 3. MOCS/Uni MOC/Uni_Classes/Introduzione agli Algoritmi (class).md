---
Academic Year: 2023/2024
Type: Uni Note
Link: https://twiki.di.uniroma1.it/twiki/view/Intro_algo/PZ/WebHome
---
---
**Lezioni:**
- vedi pdf lez8 per introduzione a sorting
- (bucket sort + fare tutti gli altri ordinamenti lineari pdf lez12)
+  heap sort
2. [[Al 1 Mag]]
3. [[Alberi Ricerca Binaria]]
4. [[Hash Table]]

##### Basi
- [[Concetti di base x Algoritmi]]

##### Studio Algoritmi
- [[Analisi Asintotica degli Algoritmi]]🟢
- [[Algoritmi Iterativi]] 🟢
- [[Esempi calcolo costo algoritmi iterativi]] 🔴
- [[Algoritmi Ricorsivi]] 🔴
- [[Risolvere e calcolare Equazione di Ricorrenza]] 🟡

##### [[Strutture Dati]]
- [[Array (Struttura Dati)]] 🟢
- [[Linked List (Struttura Dati)]] 🟡 (aggiungere codice)
- [[Pile (Struttura Dati)]] 🟢
- [[Code (Struttura Dati)]] 🟢
- [[Heap (Struttura Dati)]] 🟡 (finire costo computazionale)
- [[Alberi (Struttura Dati)]] 🟢
- [[Alberi Binari (Struttura Dati)]] 🟢
	- [[Memorizzazione tramite puntatori (Alberi Binari)]] 🟢
	- [[Rappresentazione posizionale (Alberi Binari)]] 🟢
	- [[Rappresentazione tramite vettore dei padri (Alberi Binari)]] 🟢
		- [[Visite Alberi (preorder, inorder, postorder)]] 🟡 (finire visite per livelli)
- [[Alberi Binari di Ricerca]]
- [[Hash Table]]


>[!warning] Albero bilanciato
>Quando altezza è logaritmica ovvero quando in numero di nodi è $n$ e l'altezza dell'albero è $\log(n)$ (inserisci negli appunti)

##### [[Algoritmi di Ricerca]]
1. [[Ricerca Base]] 🔴
2. [[Ricerca Binaria]]🔴

##### [[Algoritmi di Ordinamento]]
**Algoritmi $\Theta(n^{2})$:**
- [[Insertion Sort]] 🔴
- [[Selection Sort]] 🔴
- [[Bubble Sort]] 🔴

**Algoritmi $\Theta(n \log n)$:**
- [[Marge Sort]] 🟢
- [[Quick Sort]] 🟢 (sistemare solo costo computazionale)
- [[Heap Sort]] 🟡 (da finire)

**Algoritmi "Lineari":**
- [[Bucket Sort]]

**Definizione:** [[Algoritmi di Ordinamento#Stable Sorting Algoritms|Algoritmo di ordinamento Stabile]] 🟡 (Finire di sistemare)

---

Esercizio:
Scorro tutto l'albero e mi salvo il livello la foglia nel livello più alto (ovvero il livello più vicino alla radice)

```python
def es(p):
	if p==None: 
		return 0
	
	return 1 + min(es(p.left), es(p.right) 
```

```python
def es(p):
	if p.letf == None and p.right == None:  # Se il nodo è una foglia
		return 0                                # caso base

	if p.left==None and p.right!=None:      # Se esiste solo il nodo sinistro
		return es(p.right)+1

	if p.left!=None and p.right==None:      # Se esiste solo il nodo destro
		return es(p.left)+1
	
											# Se esistono tutti e due i nodi filgi
	return 1 + min(es(p.left), es(p.right)) # 
```