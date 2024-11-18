---
created: 2024-05-01
type: Uni Note
class:
  - "[[Introduzione agli Algoritmi (class)]]"
academic year: 2023/2024
related:
  - "[[Alberi Binari (Struttura Dati)]]"
  - "[[Alberi (Struttura Dati)]]"
completed: true
updated: 2024-05-27T13:29
---
---

>[!abstract] Index
>1. [[#Introduzione]]
>2. [[#Spazio]]
>3. [[#Svantaggi]]

>[!abstract] Related
>- [[Alberi Binari (Struttura Dati)]]
>- [[Introduzione agli Algoritmi (class)]]

---
## Introduzione

I nodi vengono memorizzati in un vettore, nel quale 
- La **radice** occupa la posizione di indice $0$
- Il **figlio sinistro** è in posizione $2i+1$
- Il **figlio destro**  è in posizione $2i+2$

Dove con $i$ si indica la posizione del **nodo padre**.

>[!info] Esempio
>![[signal-2024-05-01-201702_002.png|550]]
>
>**oss:** Posizione dell'elemento `f` è $\textcolor{orange}{5}$, la posizione del suo figlio sinistro `h` è $2\cdot \textcolor{orange}{5}+1=11$

>[!warning] Rappresentazione Heap
>Questa rappresentazione è utilizzata dalla [[Heap (Struttura Dati)]]

---
## Spazio
Lo spazio da allocare in memoria dipende dall'altezza dell'albero (non dal numero di nodi)

>[!warning] Formula 
>n = $2^{n+1}-1$
>
>Dove $n$ è il numero possibile di nodi di un albero con altezza $h$

---
## Svantaggi

Un Albero Binario a rappresentazione posizionale richiedi di allocare in memoria un vettore capace di rappresentare un albero completo di grandezza $2^{h+1}-1$ dove $h$ è l'altezza dell'albero.

Quindi lo spazio occupato in memoria non dipende dal numero effettivo di elementi dell'albero ma dalla lunghezza dal cammino più lungo dalla radice ad una foglia (ovvero l'altezza)

In casi di alberi poco densi questo porta a un notevole spreco di spazio

>[!info] Esempio
>![[signal-2024-05-01-203630.png|550]]
>
>**h** = 3
>**Spazio Occupata:** $2^{h+1}-1 = 2^{3+1}-1 = \textcolor{orange}{15}$
>**Spazio Utilizzato** = 4
>**Spazio inutilizzato:** 15 - 4 = 11

---
## Metodi 

**Leggi:** [[Operazioni su diverse rappresentazioni di alberi binari a confronto]]

---