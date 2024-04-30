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
>1. 

>[!abstract] Related
>- [[Strutture Dati]]
>- [[Introduzione agli Algoritmi (class)]]

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

La **Coda** è una struttura dati che esibisce un comportamento **FIFO** (Last In First Out)

>[!info] FIFO
>Gli elementi vengono prelevati dalla coda nello stesso ordine con il quale vi sono stati inseriti.

---
## Operazioni

Su una pila sono definite solo due operazioni: 
- Inserimento ([[#Enqueue (inserimento)|Enqueue]])
- Estrazione ([[#Dequeue (estrazione)|Dequeue]])

>[!warning] Head & Tail
>Per garantisce la proprietà FIFO l’operazione Enqueue opera su una estremità della coda (tail) e la Dequeue opera sull’altra estremità (head)
>
>![[signal-2024-04-25-132531_002.png|500]]

---
#### Enqueue (inserimento)

>[!info] Implementazione lista python
>
>```python
>def Inserimento(Coda, x):
>	Coda.append(x)
>```
>
>Costo: $\theta(1)$

>[!info] Implementazione linked list
>Prende in input i puntatori alla testa e alla coda ed il valore da inserire e dopo aver inserito il nodo col nuovo valore in coda restituisce i puntatori alla testa ed alla coda
>```python
>def Inserimento(testa, coda, x):
>	p = Nodo(x)
>	if coda == None
>		return p, p
>	coda.next = p
>	return testa, p
>```
>
>Costo: $\Theta(1)$
>
>Risultato operazione `p = inserimento(testa, coda, 3)`:
>![[Pasted image 20240425141337.png|500]]

---
#### Dequeue (estrazione)

>[!info] Implementazione lista python
>
>
>```python
>def Estrazione(Cosa):
>	if Pila = []: 
>		return None
>	return Pila.pop(0)
>```
>
>costo: $\theta(n)$

>[!info] Implementazione linked list
>Prende in input i puntatori alla testa e alla coda e dopo aver estratto il valore del nodo in testa lo restituisce con i puntatori alla testa ed alla coda
>
>```python
>def Estrazione(testa, coda):
>	if testa == None:                     # Caso len = 0
>		return None, None, None
>	if testa == coda:                     # Caso len = 1
>		return testa.key, None, None
>	return testa.key, testa.next, coda    # Caso len > 1
>```
>
>Costo: $\Theta(1)$
>
>Risultato operazione `x, testa, coda = estrai(testa, coda)`:
>![[Pasted image 20240425142023.png|600]]

---