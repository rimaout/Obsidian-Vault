---
type: Uni Note
class: "[[Calcolo delle Probabilità (class)]]"
academic year: 2024/2025
related:
  - "[[Variabili Aleatorie]]"
  - "[[Variabile Aleatorie Congiunte]]"
completed: true
created: 2024-12-02T10:35
updated: 2026-01-31T13:32
---
>[!abstract] Related
>- [[Variabili Aleatorie]]
>- [[Variabile Aleatorie Congiunte]]
>- [[Calcolo delle Probabilità (class)]]

---
## Introduzione

Delle variabili aleatorie si dicono indipendenti quando per ogni v.a. il valore di una non influenza il valore delle altre.

>[!note] Definizione
>Date $X_{1}, X_{2},\dots,X_{n}$ v.a. sullo stesso spazio campionario, queste sono ***indipendenti*** se:
>
>$$
>P(X_{1} \in A_{1}, \dots , X_{n} \in A_{n}) = P(X_{1}) = P(X_{1} \in A_{1}), \dots , P(X_{n} \in A_{n})
>$$
>
>$\forall A_{1}, A_{2},..,A_{n} \subset \mathbb{R}$
>
>>***Ovvero:*** Se ho un esperimento formato da sotto-esperimenti operativamente indipendenti (non si influenzano) allora variabili aleatorie che si riferiscono a sotto-esperimenti diversi sono tra loro indipendenti.

>[!example] Esempio
>Lanciamo un dado 20 volte
>
>$$
>\begin{align*}
>X & := \text{Numero uscito al 3° lancio}\\
>Y & := \text{Numero uscito al 9° lancio}\\
>Z & := \text{Numero uscito al 17° lancio}\\​
>\end{align*}
>$$
>
>Queste sono variabili indipendenti tra lore infatti il valore risultante da un lancio del dato non influenza gli altri lanci.

---
## Calcolo con v.a. congiunta

>[!note] Formula
>Siano $X: S \to \mathbb{R}$ e $Y:S \to \mathbb{R}$ v.a. discrete.
>
>- $X$ assume i valori $\{ x_{i} \}_{i\in I}$
>- $Y$ assume i valori $\{y_{j}\}_{j \in J}$
>
>$X$ e $Y$ sono indipendenti se e solo se: 
>
>$$
>P_{X,Y}(x_{i}, y_{j}) = P_{X}(x_{i}) \cdot  P_{Y}(y_{j})\ \ \ \ \forall i \in I, \,j \in J
>$$

>[!warning] Scorciatoia
>Per capire se $X$ e $Y$ sono indipendenti basta sapere $P_{X,Y}$ e non le [[Variabile Aleatorie Congiunte#Densità di probabilità Marginale|probabilità marginali]] $P_{X}$ e $P_{Y}$.
>
>Infatti:
>
>$$
>\begin{align*}
>&P_{x}(x_{i}) = \sum_{j} P_{X,Y}(x_{i},y_{j})\\
>
>&P_{Y}(y_{j}) = \sum_{i}P_{X,Y} (x_{i}, y_{j})
>\end{align*}
>$$

### Valore atteso

$$
E[XY] = E[X]\cdot  E[Y]
$$

### Varianza

$$
\text{Var}(aX + bY) = \text{Var}(aX) + \text{Var}(bY) + 2\text{Cov}(aX,bY)
$$

### Covarianza

$$
\text{Cov}(X,Y) = 0
$$
