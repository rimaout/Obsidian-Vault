---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-03-27T17:47
updated: 2025-04-02T23:30
---
## Ricerca cammini minimi su grafi con pesi anche negativi

***oss:*** grafo può essere anche non diretto

>[!danger] Cicli Negativi
>
>Per far si che l'algoritmo funzioni non ci devono essere cicli negativi

>[!warning] Proprietà
>
>Se il grafo `G` non contiene cicli negativi, allora per ogni nodo `t` raggiungibile dalla sorgente `s` esiste un cammino di costo minimo che attraversa al più `n-1` archi.
>
>Questo perché un cammino minimo non percorre mai un nodo più di una volta.
>
>***Quindi:*** Questo garantisce che il costo minimo può essere calcolato considerando solo cammini di questa lunghezza

