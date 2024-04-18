---
Created: 2024-04-18
Type: Uni Note
Class:
  - "[[Introduzione agli Algoritmi (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Strutture Dati]]"
Completed: false
---
---
## Array


Quando dichiariamo un classico array dobbiamo decidere la dimensione che non potrà mai più essere cambiata 

```c
int ANum[50]
```

Se riempiamo la capienza massima dell'array dobbiamo crearne uno nuovo (con dimensione maggiore) ed spostare tutti i dati dal vecchio array al nuovo

Inoltre un classico array può contenere un solo data type, infatti per dichiarare un array dobbiamo specificare un tipo di dato e quanti elementi allocare 

in questo caso ad ogni tipo di dato è associata un dimensione, per esempio un char occupa un byte, quindi quando allochiamo un array di 50 char stiamo allocando $50\cdot 1 \text{ byte}$ nella memoria

---
## Linked List

Le `linked list` sono composte composte da un oggetto che chiameremo nodo definito da due parametri:
- `key:` ovvero l'elemento vero e proprio
- `next:` un punitore utilizzato ad indicare il nodo successivo

>[!note] Nodo
>![[Pasted image 20240418094424.png|500]]

>[!note] Linked List
>![[Pasted image 20240418094501.png|600]]

---
## Creazione di una `linked list`

>[!danger] Tutti questi codici sono scritti in Python

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
>```python 
>def Crea(A)
>	if A==[]: return None # controllo lista vuota
>
>	p = None # origine linked list
>	q = p    # puntatore d'appoggio (punta ad ultimo elemento aggiunto)
>	
>	for e in A:
>		q = Nodo(e)
>		q = q.next
>	
>	return p
>```

>[!warning] Python Garbage Collector
>Se abbiamo una `linked list` il cui primo nodo è puntato solamente da un puntatore `p`e sovrascriviamo questo puntatore (es: `p=None`) la lista andrà "persa" (non più puntata da niente).
>- Python in questo caso si occupa di liberare la memoria (cancellando il primo nodo della lista).
>- Il secondo nodo della linked list ora non è più puntato da niente e verra "cancellato", e a sua volta accadrà la stessa cosa per il resto dei nodi della lista.

## Manipolazione delle `linked list`

>[!note] Aggiungere elemento in testa
>```python
>def Insert0(p, x):
>	
>```
>

>[!note] Aggiungere elemento in coda

>[!note] Aggiungere un elemento in posizione x
>1. Creare nuovo nodo
>2. Inizializzare il puntatore `next` del nuovo nodo uguale al puntatore `next` del puntatore nodo precedente (pos: $x-1$)
>3. Cambiare puntatore `next` del nodo precedente (pos $x-1$) con posizione del nuovo nodo 
>
>**Posizione non finale:**
>![[Pasted image 20240418095217.png|500]]

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







