---
type: Uni Note
class: "[[Calcolo delle Probabilità (class)]]"
academic year: 2024/2025
related:
  - "[[Variabili Aleatorie]]"
completed: true
created: 2024-11-30T11:02
updated: 2026-01-31T13:32
---

>[!abstract] Related
>- [[Variabili Aleatorie]]
>- [[Calcolo delle Probabilità (class)]]

---
## Variabile Aleatoria di Bernoulli

Una variabile di Bernoulli è una variabile aleatoria che può assumere solo due valori possibili, solitamente indicati come 0 e 1, o come "successo" e "fallimento".

>[!note] Definizione Matematica
>Una v.a. $X$ è detta di Bernoulli di parametro $p \in [0,1]$ se:
>- $P(X=1)=p$ 
>- $P(X=0)=1−p$

>[!warning] Osservazioni
>$$
>\begin{align*}
>&1.\ \ \textcolor{orange}{E[X]} = 1 \cdot  P(X=1) + 0 \cdot P(X=0) = \textcolor{orange}{p}\\
>&2.\ \ \textcolor{orange}{E[X^{2}]} = 1^{2} \cdot  P(X=1) + 0^{2} \cdot P(X=0) = \textcolor{orange}{p}\\
>&3.\ \ \textcolor{orange}{\text{Var}(X)} = E[X^{2}]-(EX)^{2} = p-p^{2} = \textcolor{orange}{p(1-p)}\\
>\end{align*}
>$$
