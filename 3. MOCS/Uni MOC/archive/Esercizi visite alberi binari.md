---
created: 2024-05-15
type: Uni Note
class:
  - "[[Introduzione agli Algoritmi (class)]]"
academic year: 2023/2024
related:
  - "[[Alberi (Struttura Dati)]]"
  - "[[Alberi Binari (Struttura Dati)]]"
  - "[[Visite Alberi (preorder, inorder, postorder)]]"
completed: true
updated: 2024-05-27T13:29
---
---

>[!abstract] Index
>1. [[#Applicazione delle visite]]
>2. [[#Conta Nodi]]
>3. [[#Cerca]]
>4. [[#Calcolo Altezza]]
>5. [[#Conta Livello]]

>[!abstract] Related
>- [[Visite Alberi (preorder, inorder, postorder)]]
>- [[Alberi Binari (Struttura Dati)]]
>- [[Introduzione agli Algoritmi (class)]]

---
## Applicazione delle visite
Le visite sono estremamente utili per ispezionare l’albero e dedurne delle proprietà.

A seconda delle proprietà che si vuole esaminare pò essere più utile una delle tre visite considerate

**Esempi:**
1. [[#Conta Nodi]]
2. [[#Cerca]]
3. [[#Calcolo Altezza]]
4. [[#Conta Livello]]

---
## Conta Nodi

Conta il numero di nodi presenti nell’albero binario [[Memorizzazione tramite puntatori (Alberi Binari)|rappresentato tramite puntatori]].

```python
def contaNodi(p):
	if p==None: return 0

	return contaNodi(p.left) + 1 + contaNodi(p.right)
```

>[!note] Funzionamento
>1. Se è vuoto (cioè, `p == None`), ritorna `0` e termina la funzione (caso base della ricorsione).
>2. Se l'albero non è vuoto
>	3. Chiama ricorsivamente la funzione `contaNodi(p.left)` per contare il numero di nodi nel sottoalbero sinistro.
>	4. Aggiunge `1` al conteggio per includere il nodo corrente.
>	5. Chiama ricorsivamente la funzione `contaNodi(p.right)` per contare il numero di nodi nel sottoalbero destro.
>	6. Somma i conteggi dei sottoalbero sinistro e destro e del nodo corrente, e ritorna il totale.
>
>**oss:** si basa sulla [[Visite Alberi (preorder, inorder, postorder)#Visita inordine (inorder)|visita inorder]].

---
## Cerca
Di se una determinata valore $x$ è presente all'intero di un albero $p$

```python
def cerca(p, x):
	# Se l'albero è vuoto, l'elemento non è presente
	if p == None:
		return False
	 
	# Se l'elemento corrente è uguale a x, l'elemento è stato trovato
	if p.key == x:
		return True

	# Cerca l'elemento nei sottoalbero sinistro e destro
	return cerca(p.left, x) or cerca(p.right, x)

```

>[!note]- Versione prof
>```python
>def cerca(p, x):
>	if p == None: 
>		return False
>		
>	if p.key == x: 
>		return True
>		
>	if cerca(p.left, x): 
>		return True
>		
>	return cerca(p.right, x)
>```

>[!note] Funzionamento
>La funzione controlla prima se l'albero è vuoto. Se è vuoto, ritorna False. Se il nodo corrente è uguale a x, ritorna True. Altrimenti, cerca l'elemento x nei sottoalbero sinistro e destro, chiamando se stessa ricorsivamente. Se l'elemento x è presente in uno dei sottoalbero, la funzione ritorna True. Altrimenti, ritorna False.
>
>**oss:** si basa sulla [[Visite Alberi (preorder, inorder, postorder)#Visita in preordine (preorder)|visita preorder]].

---
## Calcolo Altezza

Stabilire l'[[Alberi (Struttura Dati)#^20bd53|altezza]] di un albero binario, nota bene, se l'albero è vuoto ritornare -1, sel' albero ha un solo elemento (la radice) l'altezza è 0.

```python
def altezza(p):

    if p == None:
        return -1

    return 1 + max(altezza(p.left), altezza(p.right))
```

>[!note] Funzionamento
>1. Controlla se l'albero è vuoto (cioè, `p == None`). Se è vuoto, ritorna `-1`. Questo è il caso base della ricorsione.    
>2. Se l'albero non è vuoto, chiama ricorsivamente la funzione `altezza(p.left)` per calcolare l'altezza del sottoalbero sinistro e `altezza(p.right)` per calcolare l'altezza del sottoalbero destro. 
>3. Prende il massimo tra le altezze dei sottoalbero sinistro e destro. Questo è perché l'altezza di un albero è determinata dal sottoalbero più alto. 
>4. Aggiunge `1` al massimo delle altezze dei sottoalbero. Questo `1` rappresenta il bordo tra il nodo corrente e il sottoalbero più alto. 
>5. Ritorna il risultato.

>[!warning] Attenzione al caso 0
>Se l'albero ha un solo nodo, sia `p.left` che `p.right` saranno `None`. Quindi, le chiamate ricorsive a `altezza(p.left)` e `altezza(p.right)` ritorneranno entrambe `-1`. La funzione `max` restituirà `-1`, e l'aggiunta di `1` darà `0`, che è l'altezza corretta per un albero con un solo nodo.
>
>Quindi, la funzione `altezza` restituirà `0` per un albero con un solo nodo, come previsto.

---
## Conta Livello

Stabilire il numero di nodi presenti a un determinato livello $k$ (ricorda che la radice è a livello zero)

```python
def contaLiv(p , k):
	
	if k == 0:
		return 1
	
	if p == None:
		return 0

	return contaLiv(p.left, k-1) + contaLiv(p.right, k-1)
```

>[!note] Funzionamento
>1. Se `k` è `0`, significa che siamo al livello della radice dell'albero, quindi ritorna `1` (perché c'è esattamente un nodo, la radice, a questo livello).
>2. Se `p` è `None`, significa che abbiamo raggiunto un punto dell'albero dove non ci sono più nodi (un "albero vuoto"), quindi ritorna `0` (non ci sono nodi a questo livello).
>3. Altrimenti, fa due chiamate ricorsive alla funzione `contaLiv`: una per il sottoalbero sinistro (`p.left`) e una per il sottoalbero destro (`p.right`), entrambe con `k-1`. Questo perché quando scendiamo di un livello nell'albero, dobbiamo ridurre `k` di `1`. 
>4. Infine, somma i risultati delle due chiamate ricorsive e ritorna il totale. Questo totale rappresenta il numero totale di nodi al livello `k` nell'albero.

---