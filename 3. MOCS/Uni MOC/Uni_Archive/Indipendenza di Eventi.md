---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2024-10-21T13:48
updated: 2024-10-22T19:34
---
>[!abstract] Index
>1. 

>[!abstract] Related
>- 

---
## Introduzione

>[!note] Definizione
>Due metodi si dicono indipendenti se:
>
>$$
>E \perp\!\!\!\!\!\!\perp F \iff P(E \cap  F) = P(E) \cdot P(F)
>$$
>
>>**oss:** notazione per indipendenza $E \perp\!\!\!\!\!\!\perp F$ 

 >[!warning] Metodo Intuitivo
>$E$ e $F$ sono indipendenti se: 
>
>$$
>P(E \vert F) = P(E)\ \text{ e }\ P(F \vert E) = P(F)
>$$
>
>Questa definizione ha vale soltanto se  $P(F)>0$ e  $P(E)>0$.

>[!warning] Osservazioni
>1. se $E \perp\!\!\!\!\!\!\perp F \implies E^{c} \perp\!\!\!\!\!\!\perp F$
>2. se $P(E) = 0 \implies E \perp\!\!\!\!\!\!\perp F$ per qualsiasi $F$
>   

>[!example]- Esempio Eventi Dipendenti
>Lancio 2 volte un dado
>- $E = \text{il risultato del 1° lancio è 4}$
>- $F = \text{la somma dei lanci è 6}$
>  
>Calcolare se $E$ ed $F$ sono indipendenti:
>
>- $S = \{ (a,b): a,b \in \{ 1,2,3,4,5,6 \} \}$
>- $E = \{ 4 \}$
>- $F = \{ (a,b) \in S: a+b = 6\} = \{ (1,5), (2,4), (3,3), (4,2), (5,1) \}$
>
>Quindi:
>- $P(E) = \frac{{ \lvert E \rvert } }{{ \lvert S \rvert } } = \frac{1}{6}$
>- $P(F) = \frac{{ \lvert F \rvert } }{{ \lvert S \times S \rvert } } = \frac{5}{36}$
>- $P(E \cap F) = P(\{4,2\}) = \frac{{ \lvert \{ 4,2 \} \rvert } }{{ \lvert S \times S \rvert } } = \frac{1}{36}$
>
>Ora possiamo vedere se i due eventi sono indipendenti, utilizzando $E \perp\!\!\!\!\!\!\perp F \iff P(E \cap  F) = P(E) \cdot P(F)$:
>
>$$
>\begin{align*}
>
>P(E \cap  F) &= P(E) \cdot P(F)\\
> \frac{1}{36} &= \frac{1}{6} \cdot \frac{5}{36} \ \ \ \ (falso)
>\end{align*}
>$$
>
>Quindi visto che $P(E \cap  F) \not= P(E) \cdot P(F)$ allora $E$ e $F$ **NON** sono indipendenti.

>[!example] Esempio Eventi
>Lancio 2 volte un dado
>- $E = \text{il risultato del 1° lancio è 4}$
>- $F = \text{la somma dei lanci è 7}$
>  
>Calcolare se $E$ ed $F$ sono indipendenti:
>
>- $S = \{ (a,b): a,b \in \{ 1,2,3,4,5,6 \} \}$
>- $E = \{ 4 \}$
>- $F = \{ (a,b) \in S: a+b = 7\} = \{ (1,6), (2,5), (3,4), (4,3), (5,2), (6,1)\}$
>
>Quindi:
>- $P(E) = \frac{{ \lvert E \rvert } }{{ \lvert S \rvert } } = \frac{1}{6}$
>- $P(F) = \frac{{ \lvert F \rvert } }{{ \lvert S \times S \rvert } } = \frac{6}{36} = \frac{1}{6}$
>- $P(E \cap F) = P(\{4,3\}) = \frac{{ \lvert \{ 4,3 \} \rvert } }{{ \lvert S \times S \rvert } } = \frac{1}{36}$
>
>Ora possiamo vedere se i due eventi sono indipendenti, utilizzando $E \perp\!\!\!\!\!\!\perp F \iff P(E \cap  F) = P(E) \cdot P(F)$:
>
>$$
>\begin{align*}
>
>P(E \cap  F) &= P(E) \cdot P(F)\\
> \frac{1}{36} &= \frac{1}{6} \cdot \frac{1}{6}\\
> \frac{1}{36} &= \frac{1}{36}\ \ \ \ (\text{vero})
>\end{align*}
>$$
>
>Quindi visto che $P(E \cap  F) = P(E) \cdot P(F)$ allora $E$ e $F$ sono indipendenti.


---
## Indipendenza tra 3 Eventi

>[!warning] Teorema
>Se $E,F,G$ sono indipendenti, allora $E$ è indipendente da ogni evento costruito a partire da $F$ e $G$ usando: unione, intersezione, complementare.
>
> ---
>
>**Definizione:** Dati 3 eventi $E,F,G$ si dice che sono indipendenti se:
>- $P(E\cap F) = P(E) \cdot P(F)$
>- $P(E\cap G) = P(E)\cdot P(G)$
>- $P(F \cap G) = P(F) \cdot P(G)$
>- $P(E \cap F\cap G) = P(E)\cdot P(F) \cdot P(G)$

---

## Formula Generalizzata 

>[!note] Formula
>
>Dati $n$ eventi $E_{1},\dots ,E_{n}$, questi sono detti indipendenti se:
>
>$\forall A \subset \{ 1,2,\dots,n \}$  con $A \not = \emptyset$ allora:
>
>$$
>P \big(\bigcap E_{i}) = \prod_{i\in A} P(E_{i})
>$$