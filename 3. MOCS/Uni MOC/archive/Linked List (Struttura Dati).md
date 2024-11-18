---
created: 2024-04-23
type: Uni Note
class:
  - "[[Introduzione agli Algoritmi (class)]]"
academic year: 2023/2024
related:
  - "[[Strutture Dati]]"
completed: false
updated: 2024-06-03T20:14
---
---

>[!abstract] Index
>1. [[#Definizione]]
>2. [[#Struttura]]
>3. [[#Operazioni]]
>4. [[#Esempi]]

>[!abstract] Related
>- [[Strutture Dati]]
>- [[Introduzione agli Algoritmi (class)]]

---
## Definizione
La lista semplice (o lista concatenata) è una struttura dati nella quale gli elementi sono organizzati in successione.

>[!abstract] Proprietà
>- L'accesso avviene sempre ad una estremità della lista, per mezzo di un puntatore alla testa della lista;
>- Ogni elemento contiene un puntatore che consente l’accesso all’elemento successivo;
>- È permesso solo un **accesso sequenziale** agli elementi

---
## Struttura

Le `linked list` sono composte composte da un oggetto che chiameremo nodo definito da due parametri:
- `key:` ovvero l'elemento vero e proprio
- `next:` un puntatore utilizzato per indicare il nodo successivo

>[!note] Nodo
>![[Pasted image 20240418094424.png|350]]

>[!note] Linked List
>![[Pasted image 20240418094501.png|600]]

---
## Operazioni

>[!info]
>1. [[#Creazione]]
>2. [[#Inserimento]]
>3. [[#Eliminazione]]
>4. [[#Ricerca]]

>[!danger] Tutti questi codici sono scritti in Python

---
#### Creazione

>[!note] Definizione `Nodo` di una `linked list`
>
>```python
>class Nodo:
>	# Constructor
>	def __init__(self, key=none, next=none):
>		self.key = next
>		self.next = next
>```

>[!note] Creazione di una `linked list`
> da fare

>[!warning] Python Garbage Collector
>Se abbiamo una `linked list` il cui primo nodo è puntato solamente da un puntatore `p`e sovrascriviamo questo puntatore (es: `p=None`) la lista andrà "persa" (non più puntata da niente).
>- Python in questo caso si occupa di liberare la memoria (cancellando il primo nodo della lista).
>- Il secondo nodo della linked list ora non è più puntato da niente e verra "cancellato", e a sua volta accadrà la stessa cosa per il resto dei nodi della lista.

---
#### Inserimento

>[!note] Aggiungere elemento in testa
>```python
>def Insert0(p, x):
>	# p: puntatore 1° nodo lista
>	# x: elemento da aggiungere in testa alla lista
>	
>	q = p
>	p = Nodo(x, q)
>	return p
>```
>**note:** scritto da me, non dal prof

>[!note] Aggiungere elemento in coda

>[!note] Aggiungere un elemento in posizione x
>1. Creare nuovo nodo
>2. Inizializzare il puntatore `next` del nuovo nodo uguale al puntatore `next` del puntatore nodo precedente (pos: $x-1$)
>3. Cambiare puntatore `next` del nodo precedente (pos $x-1$) con posizione del nuovo nodo 
>
>**Posizione non finale:**
>![[Pasted image 20240418095217.png|500]]


---
#### Eliminazione
Cancella la prima occorrenza di un valore `x` nella list `p`

```python
def Cancella(p, x):
	if p = None:    # Lista Vuota
		return p

	if p.key == x:
		p = p.next
		
	else:
		q = p
		while q.next != None and q.next.key != x:
			q = q.next
		
		if q.next != None:
			q.next = q.next.next
		
	
```

**Costo:** $O(n)$

---
#### Ricerca



---
## Esempi

>[!note] Creazione di una lista
>```python
P = Nodo(7)
P.next = Nodo(2)
P.next.next = Nodo(12)
>```

>[!note] Print di una lista
>```python
>def Stampa(p):
>	while p != null:
>		print(p.key)
>		p = p.next
>```
>**note:** p is local variable and doesn’t change the original p
