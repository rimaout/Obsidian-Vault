---
created: 2024-04-30
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
>1. [[#Introduzione]]
>2. [[#Nodi (definizioni)]]
>3. [[#Esempio]]
>4. [[#Alberi Ordinati]]

>[!abstract] Related
>- [[Strutture Dati]]
>- [[Introduzione agli Algoritmi (class)]]

---
## Introduzione 
L’albero è una struttura dati estremamente versatile, utile per modellare una grande quantità di situazioni reali e progettare le relative soluzioni algoritmiche.

>[!info] Nodi e Archi
>L’albero in informatica è una struttura dati che rappresenta un insieme di nodi interconnessi da archi. È formato da due 
>- **Nodo** contiene informazioni
>- **Arco** stabilisce un collegamento gerarchico fra due nodi. 

>[!info] Livelli
>I nodi sono organizzati in **livelli**, numerati in ordine crescente allontanandosi dalla [[#^b6379b|radice]].

>[!info] Altezza
>L'**Altezza** di un albero è la lunghezza del più lungo cammino dalla [[#^b6379b|radice]] ad una [[#^5dff15|foglia]].
>- Una albero di altezza $h$ contiene $h+1$ livelli, numerati da $0$ a $h$.

^20bd53

---
## Nodi (definizioni)

>[!info] Radice
>La radice di un albero in informatica è il nodo più alto dell’albero (livello 0), rappresentante l’origine del tutto.
>- Non ha un padre o fratelli
>- È l'unico antenato comune ti tutti i nodi
^b6379b

>[!info] Padre
>Dato un qualunque nodo `v` che non sia la radice, il primo nodo che si incontra sul cammino da `v` alla radice viene detto **padre** di `v`.

>[!info] Fratelli
>Nodi che hanno lo stesso padre sono detti **fratelli**.
>- La radice è l’unico nodo che non ha padre.

>[!info] Antenato
>Ogni nodo sul cammino da `v` alla radice viene detto **antenato** di `v`.

>[!info] Figli
>Tutti i nodi che hanno `v` come padre sono detti **figli** di `v`.

>[!info] Foglie
>I nodi che non hanno figli sono dette **foglie**.
^5dff15

>[!info] Discendenti
>Tutti i nodi che ammettono `v` come antenato vengono detti discendenti di `v`.

---
## Esempio

![[Pasted image 20240501114121.png|700]]

---
## Alberi Ordinati

Un albero si dice ordinato se attribuiamo un qualche ordine ai figli di ciascun nodo.

Se un nodo ha $k$ figli, allora vi è un figlio che viene considerato primo, uno che viene considerato secondo, …, uno che viene considerato k-esimo.

Una particolare sottoclasse di alberi radicati e ordinati è quella degli [[Alberi Binari (Struttura Dati)|Alberi Binari]], che hanno la particolarità che ogni nodo ha al più due
figli.

---