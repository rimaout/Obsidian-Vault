---
type: Uni Note
class: "[[Calcolo delle Probabilità (class)]]"
academic year: 2024/2025
related:
  - "[[Variabili Aleatorie]]"
completed: true
created: 2024-11-30T11:19
updated: 2025-02-17T17:11
---
>[!abstract] Related
>- [[Variabili Aleatorie]]
>- [[Calcolo delle Probabilità (class)]]

---
## Variabile Geometrica

Una variabile aleatoria geometrica è una variabile aleatoria che rappresenta il numero di prove necessarie per ottenere il primo successo in una sequenza di prove indipendenti, ognuna delle quali ha una probabilità di successo costante.

>[!note] Notazione
>Indichiamo una v.a. geometrica $X$ di parametro $p$ con:
>
>$$
>X = \text{Geom}(p)
>$$
>
>Dove $p$ indica la probabilità di successo in ogni prova.

---
## Formule

>[!danger] Densità di Probabilità Discreta
>
>La probabilità di ottenere il primo successo alla $k$-esima prova è data dalla formula:
>
>$$
>P(X=k) = (1-p)^{k-1} \cdot p
>$$
>
>>**oss:** $P(k = \infty ) = 0\ \ \to\ \  \text{probabilità che non ci sia mai un successo}$ 
>

>[!danger] Valore Atteso
>$$
>E[X] = \frac{1}{p}
>$$
>

>[!danger] Varianza
>$$
>\text{Var}(X) = \frac{1-p}{p^{2}}
>$$
>

---
## Esempi

>[!example]- Esempio 1
>
>Supponiamo di avere una moneta truccata che ha una probabilità di testa del 20% ($p = 0,2$). Sia $X$ la variabile aleatoria che rappresenta il numero di lanci necessari per ottenere la prima testa.
>
>Determinare:
>1. Probabilità di ottenere la prima testa al primo lancio
>2. Probabilità di ottenere la prima testa al secondo lancio
>3. Probabilità di ottenere la prima testa al terzo lancio
>4. Valore atteso di $X$
>5. Varianza di $X$
>
>**1. Probabilità di ottenere la prima testa al primo lancio:**
>
>$$
>P(X=1) = (1-p)^{1-1} \cdot p = p = 0,2
>$$
>
>**2. Probabilità di ottenere la prima testa al secondo lancio:**
>
>$$
>P(X=2) = (1-p)^{2-1} \cdot p = (1-p) \cdot p = 0,16
>$$
>
>**3. Probabilità di ottenere la prima testa al terzo lancio:**
>
>$$
>P(X=3) = (1-p)^{3-1} \cdot p = (1-p)^2 \cdot p = 0,128
>$$
>
>**4. Valore atteso di $X$:**
>
>$$
>E[X] = \frac{1}{p} = \frac{1}{0,2} = 5
>$$
>
>**5. Varianza di $X$:**
>
>$$
>\text{Var}(X) = \frac{1-p}{p^2} = \frac{1-0,2}{0,2^2} = 20
>$$

>[!example]- Esempio 2
>Lanciamo un dado fino a quando esce il numero 6.
>
>**Calcolare il valore atteso del numero di lanci effettuati:**
>- $X = \text{Lanci effettuati fino al primo 6} = Geom(p)$
>- $p = P(\text{esce 6}) = \frac{1}{6}$
>
>$$
>E[X] = \frac{1}{\frac{1}{p}} = \frac{1}{\frac{1}{6}} = 6
>$$
>
>**Calcolare la probabilità di aver effettuato almeno 7 lanci:**
>
>$$
>P(X=7) = (p)^{k-1} = \left( \frac{5}{6} \right)^{6}
>$$
