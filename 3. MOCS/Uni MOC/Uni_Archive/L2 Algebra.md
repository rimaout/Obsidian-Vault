---
type: Uni Note
class: 
academic year: 2023/2024
related: 
completed: false
created: 2024-09-25T17:15
updated: 2024-09-26T16:24
---
>[!abstract] Index
>1. 

>[!abstract] Related
>- 

---

## Prodotto cartesiano

>[!note] Definizione Matematica
>
>$$
>X \times Y = \{ (x,y): x \in X, y \in Y \}
>$$
>dove $X \not= \emptyset, \ \ Y \not= \emptyset$

 >[!warning] oss
>$$
>\begin{align*}
>&-\ \mathbb{R}^{2}  = \mathbb{R} \times \mathbb{R}\\
>&-\ \mathbb{R}^{n}  = \mathbb{R} \times \mathbb{R}^{n-1}\\
>\end{align*}
>$$

---
## Corrispondenza 

Mette in relazione 2 insiemi non vuoti 


>[!note] definizione Matematica
>$$
>(X, Y, \Gamma) \subset (X, Y, X \times Y)
>$$
>
>Dove $X,Y,\Gamma \not= \emptyset$ e $\Gamma \subset X\times Y$

>[!warning] oss
>$X$ è chiamato dominio
>$Y$ è chiamato codominio

## Relazione

una relazione è una corrispondenza dove $Y = X$ quindi:

$$
R = (X, \Gamma) = (X, X, \Gamma)
$$

Dove $\Gamma = X^{2} = X \times X$


#### Proprietà

>[!warning] Riflessiva
>R si dice riflessiva se $\forall x \in X, x\ R\ x$
>
>Ovvero: $\forall x \in X, (x,x) \in \Gamma$

>[!warning] Simmetrica
>R si dice simmetrica se $\forall x,y \in X$ se $x R y$
>
>Ovvero: $\forall (x,y) \in \Gamma \implies (y,x) \in \Gamma$

>[!warning] Transitiva
>R si dice riflessiva se $\forall x, y, z \in X,\  (x R y\ \ e\ \ y R x \implies x R z)$

>[!warning] Equivalenza
>Se una relazione rispetta le proprietà allora si dice Di Equivalenza

---
## Esempi relazioni di equivalenza

>[!note] Relazione di Uguaglianza
>Una relazioni di uguaglianza è la più semplice relazione di equivalenza
>
>$$
>R = (\mathbb{R}, \Delta)
>$$
>Dove$\Delta = \{ (x,x): x \in \mathbb{R} \}$
>
>se $x R y \iff x = y$
>- è riflessiva $\forall x \in \mathbb{R}, x = x$
>- è simmetrica ...
>- è transitiva ....

>[!note] Rette parallele
>- $X = \{ \text{rette di }\mathbb{R}^{2} \}$
>- $r, r' \in X$
>- $r \mid\mid r' \iff r\text{ e } r' \text{sono parallele}$
>
>Proprietà:
>- è riflessiva: $\text{ogni retta è parallela con sestesa}$
>- è simmetrica: $\text{se } r \mid\mid r' \text{ sono parallele}$
>- è transitiva: $r\mid\mid r' \wedge r' \mid r''$

>[!note] Relazione di disuguaglianza
>$$
>x\leq y, \forall x,y \in \mathbb{R}
>$$
>
>- è riflessiva
>- è simmetrica
>- è transitiva
>- è **Totale**

>[!warning] Relazione totale
>Una relazione si dice totale quando ....

>[!warning] Relazione di inclusione
>Notare che $\subset$ è una relazione su $\{ Y: y \in X \}$ è come $\leq$, riflessiva, simmetrica e transitiva

## Studio delle relazioni di equivalenza
Sia  una relazione di equivalenza.

$$
Cl(x) = \{ y \in X\ \  t.c.\ \ x Ry \} \subset X
$$
dove $x \in X$

notare che $Cl(X) \not = \emptyset$

$Cl(x)$ è la classe di equivalenza di $x$ e $x$ è un rappresentante di quella classe.

Alter notazioni per $Cl(x)$ sono:
- $[x]$
- $[x]_{R}$


## Proposizione

data una relazione di equivalenza $R = (X, \Gamma)$

1. $x,y \in X$ allora $Cl(x) = Cl(y) \iff xRx$
2. $\forall x,y \in X$ allora:
	- o $Cl(x) = Cl(y)$
	- oppure $Cl(x) \cap Cl(y) = \emptyset$ (elementi disgiunti)

in particolare data una classe di equivalenza .....


>[!danger] Dimostrazione
>$Cl(x) = Cl(y)$ siccome $y \in Cl(y)$ ($R$ è riflessiva) si h che $y\in Cl(x)$
>
>$\implies y\in Cl(x) \implies x Ry$

---

- $X  = \emptyset$
- $\mathbb{P}$ è un insieme di sotto insiemi di $X$

$p \in \mathbb{P} \implies P \subset X$

>[!warning] Esempio
>$$
>P(X) := \{ P: P \subset X \} \text{ insime delle parti di } X
>$$
>
>Si ha che $P \in x$
