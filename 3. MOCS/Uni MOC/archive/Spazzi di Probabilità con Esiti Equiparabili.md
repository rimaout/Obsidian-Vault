---
type: Uni Note
class:
  - "[[Calcolo delle Probabilità (class)]]"
academic year: 2024/2025
related: "[[Definizioni e Assiomi della Probabilità#Spazio di Probabilità]]"
completed: false
created: 2024-10-13T13:35
updated: 2025-02-05T09:22
---
>[!abstract] Index
>1. [[#Introduzione]]
>2. [[#Proposizione]]
>3. [[#Esempi]]

>[!abstract] Related
>- [[Calcolo delle Probabilità (class)]]
>- [[Definizioni e Assiomi della Probabilità#Spazio di Probabilità|Spazio di Probabilità]]

---
## Introduzione

>[!note] Premesse
>- Supponiamo che $S$ uno spazio campionari con un numero finito $n$ di esiti.
>- Gli esiti di $S$ sono tutti **equi-probabili**, la il valore della probabilità lo chiamiamo $z$. 
>  
>$$
>P(E_{1}) = P(E_{2}) = \dots = P(E_{n}) = z
>$$
>
>>**oss:** $P(S) = 1$

>[!note] Conseguenze
>La probabilità dello spazio campionario non è altro la somma tra tutte le probabilità degli eventi che lo compongono
>
>$$
>P(S) = \sum^{n}_{i=1} P(E_{i}) = 1
>$$
>
>>**oss:** $\forall  E \in S,\ \ P(E) = k$
>
>$$
>P(S) = \sum^{n}_{i=1} z = z \cdot  n = 1
>$$
>
>Quindi visto che $z\cdot n = 1$ sappiamo che:
>
>$$
>\begin{align*}
>&- \ \ \ \ z =\frac{1}{n} \\
>&- \ \ \ \ P(E) = \frac{1}{n} \ \ (\forall E \in S)
>\end{align*}
>$$

---
## Proposizione

Se ${ \lvert S \rvert } = n$ e gli esiti sono equiparabili, allora:

$$
\forall E,\ \ P(E) = \frac{{ \lvert E \rvert }  }{{ \lvert S \rvert }  } = \frac{\# \text{ esiti favorevoli ad E}}{\# \text{ esiti possibili}}
$$

>[!warning]- Dimostrazione
>Dato $E = \bigcup_{S \in E} \{ S \}$ gli eventi $\{ S \}$, con $S \in E$ sono 2 a 2 incompatibili. Possiamo applicare l’additività finita e ottenere:
>
>$$
>P(E) = \sum_{S\in E} P(\{ S \}) = \sum_{S\in E} \frac{1}{n} = \frac{{ \lvert E \rvert }  }{n} = \frac{{ \lvert E \rvert }  }{{ \lvert S \rvert }  }
>$$

---
## Esempi

>[!example] Esempio 1
>Lanciando due dati (normali), qual'è la probabilità che la somma dei numeri sia 6?
>
>$S = \{1,2,3,4,5,6\} \times \{1,2,3,4,5,6\}$
>$E = \{ (a,b)\in S: a+b =6 \} = \{ (1,5), (2,4), (3,3), (4,2), (5,1) \}$ 
>
>$$
>P(E) = \frac{\mid E \mid}{\mid S \mid} = \frac{5}{6 \cdot  6} = \frac{5}{36}
>$$

>[!example] Esempio 2
>Ho un mazzo da 40 carte. Estraggo 2 carte senza ri-inserirle nel mazzo. Qual'è la probabilità di estrarre 2 carte di bastoni.
>
>$M = mazzo$
>$S = \{ (a,b): a,b \in M, a \not=b \}$
>
>$$
>P(E) = \frac{\mid E \mid}{\mid S \mid}
>$$
>
>Nel nostro caso:
>- $\mid S\mid$ = $40 \cdot 39$
>- $\mid E \mid$ = $10 \cdot 9$
>
>Quindi: 
>$$
>P(E) = \frac{\mid E \mid}{\mid S \mid} = \frac{10\cdot  9}{40 \cdot 39} = \frac{1}{4} \cdot  \frac{3}{13} = \frac{3}{52}
>$$

>[!example] Esempio 3
>Ho un’urna con 6 palline bianche e 5 nere. Estraggo 3 palline a caso senza rimpiazzo, quant’è la probabilità che esca 1 bianca e 2 nere?
>
>Non ci conviene registrare soltanto il colore delle palline, **questo perché rompe la simmetria**, ci conviene invece numerarle una per una in modo da distinguerle (cambio spazio campionario)
>
>$Urna = U = \{ B_{1}, B_{2}, B_{3},B_{4};B_{5},B_{6},N_{1},N_{2},N_{3},N_{4},N_{5} \}$
>
>$S = \{ A \subset U: \lvert A \rvert =  3\}$
>
>>**oss:** Un esempio di esito $A$ è $\{ B_{2},B_{4},N_{3} \}$
>
>$$
>P(E) = \frac{{\lvert E \rvert}}{{\lvert S \rvert}}
>$$
>
>${ \lvert E \rvert }  = 6 \cdot \binom{5}{2}$
>${ \lvert S \rvert } = \binom{11}{3}$ 
>
>Dove:
>- 6 è il numero di modi per estrarre una pallina bianca
>- $\binom{5}{2}$ è il modo di estrarre 2 palline nere (senza considerare l'ordine)
>
>Quindi:
>$$
>P(E) = \frac{6 \cdot  \binom{5}{2} }{\binom{11}{3} } = \frac{4}{11}
>$$
