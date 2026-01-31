---
created: 2024-03-23
type: Uni Note
class:
  - "[[Algoritmi 1 (class)]]"
academic year: 2023/2024
related:
  - "[[Risoluzione Equazione di Ricorrenza]]"
completed: true
updated: 2026-01-31T13:32
---
---

>[!info] Index
>1. [[#Introduzione]]
>2. [[#Metodo]]
>3. [[#Esempi]]

---
## Introduzione

Il Metodo degli Alberi di Ricorsione è un metodo alternativo al [[Metodo Iterativo (algoritmi ricorsivi)]], che ci permette di rappresentare graficamente le chiamate ricorsive fatte da un algoritmo per poi studiarne il costo.

---
## Metodo 

Il Metodo degli Alberi di Ricorsione è basato suddiviso in due step
1. [[#^f41677|Rappresentazione dell'albero ricorsivo]]
2. [[#^dd9001|Analisi dell'albero ricorsivo]]

>[!note] Rappresentazione dell'albero ricorsivo
>Un albero non è altro che un [[Grafo]] dove:
>- I **nodi** rappresentano il costo di ogni problema (chiamata)
>- Gli **archi** rappresentano i sotti problemi generati da ogni problema
>
>Solitamente basta rappresentare 3 livelli di ogni algoritmo per avere abbastanza informazioni per capire come si comporta ad infinto

^f41677

>[!note] Analisi dell'albero ricorsivo
>Una volta disegnato l'albero ricorsivo serve studiarlo ponendosi queste 5 domande:
>
>1. Quanti nodi ci sono per ogni generico livello $i$
>2. Qual'è il costo di un singolo nodo ad ogni generico livello $i$
>3. Qual'è il costo di un generico livelli $i$ 
>	- somma del costo di tutti i sui no
>4. Qual'è il numero di livelli di un algoritmo
>	- Calcolare numero di iterazione ($i$) per raggiungere caso base
>5. Qual'è il costo complessivo dell’algoritmo
>	- Soma del costo di di tutti i livelli

^dd9001

---
## Esempi