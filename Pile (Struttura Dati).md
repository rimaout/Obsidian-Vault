---
Created: 2024-04-23
Type: Uni Note
Class:
  - "[[Introduzione agli Algoritmi (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Strutture Dati]]"
Completed: true
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

La pila è una struttura dati che esibisce un comportamento LIFO (Last In First Out)

>[!info] LIFO
>Gli elementi vengono prelevati dalla pila nell’ordine inverso rispetto a quello col quale vi sono stati inseriti.

---
## Operazioni

Su una pila sono definite solo due operazioni: 
- Inserimento ([[#Push]])
- Estrazione ([[#Pop]])

---
#### Push

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
>![[Pasted image 20240423175423.png|450]]

---
#### Pop

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
>![[Pasted image 20240423182827.png|450]]


---