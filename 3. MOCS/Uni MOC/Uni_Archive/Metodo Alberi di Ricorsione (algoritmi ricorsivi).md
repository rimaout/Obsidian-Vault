---
Created: 2024-03-23
Type: Uni Note
Class:
  - "[[Algoritmi 1 (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Risoluzione Equazione di Ricorrenza]]"
Completed: false
---
---

>[!info] Index
>1. [[#Introduzione]]
>2. [[#Metodo]]
>3. [[#Esempi]]

---
## Introduzione

Il Metodo degli Alberi di Ricorsione è un metodo alternativo al [[Metodo Iterativo (algoritmi ricorsivi)]], che ci permette di rappresentare graficamente le chiamate ricorsive fatte da un algoritmo per poi studiarne il costo

>[!note] Albero di ricorsione
>Un albero di ricorsione è un albero in cui ogni nodo rappresenta il costo di un sotto problema in base alla specifica chiamata ricorsiva

---
## Metodo 

1. Disegnare l'albero di ricorsione, disegnando almeno tre livelli per poi andare ad infinito
2. Porsi queste 5 domande:
	- Quanti nodi ci sono al livello $i$
	- Qual'è il costo di un nodo a livello $i$
	- Qual'è il costo complessivo di tutti i nodi a livello $i$ ($numero\ nodi\cdot costo\ di\ ogni\ nodo$)
	- Qual'è il numero di livelli
3. Trovare il costo complessivo di $T(n)$

---
## Esempi