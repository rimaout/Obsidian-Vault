---
created: 2024-04-23
type: Uni Note
class:
  - "[[Introduzione agli Algoritmi (class)]]"
academic year: 2023/2024
related:
  - "[[Strutture Dati]]"
completed: true
updated: 2024-05-27T13:29
---
---

>[!abstract] Index
>1. [[#Definizione]]
>2. [[#Operazioni]]
>3. [[#Push]]
>4. [[#Pop]]

>[!abstract] Related
>- [[Introduzione agli Algoritmi (class)]]
>- [[Strutture Dati]]

---
## Definizione 

La **Pila** è una struttura dati che esibisce un comportamento **LIFO** (Last In First Out)

>[!info] LIFO
>Gli elementi vengono prelevati dalla pila nell’ordine inverso rispetto a quello col quale vi sono stati inseriti.

---
## Operazioni

Su una **Pila** sono definite solo due operazioni: 
- Inserimento ([[#Push (inserimento)|Push]])
- Estrazione ([[#Pop (estrazione)|Pop]])

>[!warning] Top
>Per garantire la proprietà LIFO le operazioni Push e Pop operano sulla stessa estremità della pila (attraverso il puntatore top)
>
>![[signal-2024-04-25-131903.png|50]]

---
#### Push (inserimento)

>[!info] Implementazione lista python
>
>```python
>def push(Pila, x):
>	Pila.append(x)
>```
>
>costo: $\theta(1)$

>[!info] Implementazione linked list
> Riceve il puntatore alla cima della pila ed il valore da inserire, lo inserisce in un nodo in cima alla lista puntata e restituisce la nuova cima
>```python
>def push(top, x):
>	return Nodo(x, top)
>```
>
>Costo: $\Theta(1)$
>
>Risultato operazione `top = push(top, 3)`:
>![[Pasted image 20240423175423.png|450]]

---
#### Pop (estrazione)

>[!info] Implementazione lista python
>
>
>```python
>def pop(Pila):
>	if Pila = []: 
>		return None
>	return Pila.pop()
>```
>
>costo: $\theta(1)$

>[!info] Implementazione linked list
>Prende il puntatore alla cima della pila e restituisce il valore del nodo in cima alla pila e la nuova cima della pila.
>
>```python
>def pop(top):
>	if pop == None:
>		return None, None
>	return top.key, top.next
>```
>
>Costo: $\Theta(1)$
>
>Risultato operazione `x, top = pop(top)`:
>![[Pasted image 20240423182827.png|450]]


---