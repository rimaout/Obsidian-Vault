---
type: Uni Note
class:
  - "[[Algoritmi 2 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-03-05T08:37
updated: 2026-01-31T13:32
---
## Rappresentazione tramite matrici binarie

Dato un grafo diretto, se `M[i][j] = 1` allora i nodi `i` e `j` sono uniti da un arco diretto che va da `i` a `j`.

>***oss:*** in un grafo non diretto avremo che `M[i][j] = M[j][i]`.

![[Pasted image 20250228171310.png|250]]

>[!note] Calcolare Grado di un nodo `x`
>
>- Calcolare il grado **entrante** di un nodo `x` dobbiamo sommare tutti gli uno, della colonna `x`, costo $\Theta(n)$.
>- Calcolare il grado **uscente** di un nodo `x` dobbiamo sommare tutti gli uno, della riga `x`, costo $\Theta(n)$.

---
## Rappresentazione tramite liste di adiacenza

Per rappresentare un grafo è possibile utilizzare un lista di liste. Dove
- la lista `G` ha tanti elementi quanto i nodi del grafo
- la lista `G[X]` è una lista contenente i nodi adiacenti al nodo `x`

![[Pasted image 20250302131843.png|500]]

>[!note] Calcolare il grado un nodo `n`
>
>Dobbiamo vedere la lunghezza della lista `G[X]`, con costo $\Theta(n)$.

>[!warning] Vantaggi e Svantaggi
>- **Vantaggio:** Notevole risparmio di spazio nel caso di grafi sparsi
>- **Svantaggio:** Vedere se due nodi sono connessi o meno può costare ora anche `O(n)`
