---
created: 2023-10-26
type: Uni Note
class:
  - "[[Metodi matematici per l'informatica (class)]]"
academic year: 2023/2024
related: 
completed: false
updated: 2024-05-27T13:29
---
---
## Index
1. [[]]

---

$$\sum_{i=0}^{n}i=\frac{{n(n+1)}}{2}$$
Gauss ha trovato questa formula a 8 anni 🤡

---
## Dimostrazione per induzione della sommatoria
**Dimostrare:** $$\sum_{i=0}^{n}i=\frac{{n(n+1)}}{2}\ \ \ \ \ \forall n\in \mathbb{N}$$
**Caso Base:** $$P(0)= \sum_{i=0}^{0}i=\frac{{n(n+1)}}{2}$$
**Ipotesi Induttiva:** $$ \begin{align}
&P(n)= \sum_{i=0}^{n}i=\frac{{n(n+1)}}{2}\\

& P(n+1)=\sum_{i=0}^{n+1}i=\textcolor{orange}{\frac{{(n+1)(n+2)}}{2}}\\
\end{align}$$
**Dim:** $$\begin{align}

& P(n+1)=\sum_{i=0}^{n+1}i=\sum_{i=0}^{n}i+(n+1)= \\
&\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ = \frac{{n(n+1)}}{2}+n+1= \frac{{n(n+1)+2(n+1)}}{2}= \\
& \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ = \textcolor{orange}{\frac{{(n+1)(n+1)}}{2}}\\
\end{align}$$
