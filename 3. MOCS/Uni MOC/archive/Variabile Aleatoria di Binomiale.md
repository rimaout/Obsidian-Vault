---
type: Uni Note
class: "[[Calcolo delle Probabilità (class)]]"
academic year: 2024/2025
related:
  - "[[Variabile Aleatoria di Binomiale]]"
completed: false
created: 2024-11-30T11:05
updated: 2024-11-30T11:36
---
>[!abstract] Related
>- [[Variabile Aleatoria di Binomiale]]
>- [[Variabile Aleatoria di Poisson#Approssimazione di variabile di Binomiale con Poisson|Approssimazione di variabile di Binomiale con Poisson]]
>- [[Variabili Aleatorie]]
>- [[Calcolo delle Probabilità (class)]]

---
## Variabile Aleatoria Binomiale

Una **variabile aleatoria binomiale** è una variabile aleatoria che rappresenta il *numero di successi in una sequenza di prove indipendenti*, ognuna delle quali ha due possibili risultati: successo o insuccesso.

La variabile aleatoria binomiale è caratterizzata da due parametri:
* $n$ -> il numero di prove
* $p$ -> la probabilità di successo in ogni prova

La variabile aleatoria binomiale può assumere valori interi compresi tra $0$ e $n$, dove $0$ rappresenta il numero di successi in nessuna delle prove e $n$ rappresenta il numero di successi in tutte le prove.

>[!note] Notazione
>Indichiamo una v.a binomiale $X$ di parametri $n,p$ con:
>$$
>X = \text{Bin}(n,p)
>$$

>***Vedi:*** [[Variabile Aleatoria di Poisson#Approssimazione di variabile di Binomiale con Poisson|Approssimazione di variabile di Binomiale con Poisson]]

---
## Formule

>[!danger] Densità di Probabilità Discreta
>La probabilità di ottenere $k$ successi in $n$ prove è data dalla formula:
>
>$$
>P(X=k) = \binom{n}{k}\cdot  p^k \cdot  (1-p)^{n-k}
>$$
>
>>[!warning]- Dim (da fare)

>[!danger] Valore Atteso
>$$
>E[X] = n \cdot p
>$$
>>[!warning]- Dim (da fare)

>[!danger] Varianza
>$$
>\text{Var}(X) = n\cdot p\cdot (1−p)
>$$
>>[!warning]- Dim (da fare)

---
## Esempi

>[!example]- Esempio 1
>Lancio cinque volte una moneta. Sia $X$ v.a definita come $X:=\text{Teste Uscite}$
>
>Determinare:
>1. Probabilità discreta di $X$
>2. $E[X]$
>3. $\text{Var}(X)$
>4. $\sigma(X)$
>   
>**oss:** $X$ è una v.a. binomiale infatti possiamo definirla come: $X = \text{Bin}\left( 5, \frac{1}{2} \right)$
>
>**1.  Probabilità Discreta:**
>Sappiamo che $X$ può assume i valori $0,1,2,3,4,5$ quindi per questi valori $k$ calcoliamo:
>$$
>\begin{align*}
>P(X=k) &= \binom{n}{k} \cdot  p^{k} \cdot (1-p)^{n-k}\\
>& \ \ |\\
>&= \binom{5}{k}\cdot  (\frac{1}{2})^{k} \cdot (\frac{1}{2})^{5-k} \\
>& \ \ |\\
>&= \binom{5}{k}\cdot  (\frac{1}{2})^{5} \\
>& \ \ |\\
>&= \binom{5}{k}\cdot\frac{1}{32} \\
>\end{align*}
>$$
>
>$$
>P(0) = \binom{5}{0}  \cdot  \frac{1}{32} = \frac{1}{32} \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ P(1) = \binom{5}{1}  \cdot  \frac{1}{32} = \frac{5}{32} \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ P(2) = \binom{5}{2}  \cdot  \frac{1}{32} = \frac{10}{32}
>$$
>
>$$
>P(3) = \binom{5}{3}  \cdot  \frac{1}{32} = \frac{10}{32} \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ P(4) = \binom{5}{4}  \cdot  \frac{1}{32} = \frac{5}{32} \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ P(5) = \binom{5}{2}  \cdot  \frac{1}{32} = \frac{1}{32}
>$$
>
>**2. Valore Atteso:** $E[X] = n\cdot p = 5 \cdot \frac{1}{2} = 2.5$
>
>**3. Varianza:** $\text{Var}(X) = n \cdot p \cdot (1-p) = 5 \cdot \frac{1}{2} \cdot \frac{1}{2} = 1.25$
>
>**4. Deviazione Quadrata:**  $\sigma(X) = \sqrt{ \text{Var}(X) } = \sqrt{ 1.25 } = 1.118$
