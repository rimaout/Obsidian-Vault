---
Created: 2024-03-04
Type: Uni Note
Class: 
Academic Year: 2023/2024
Related: 
Completed: false
---
---
## Index
1. [[]]

---
$$
\sum^{+\infty }_{n=1}= \frac{1}{n} = +\infty 
$$


## Serie Armonica  Generalizzata 
$$
\sum^{+\infty }_{n=1} \frac{1}{n^{\alpha}}
$$

>[!warning] oss
>Se $\alpha\leq 1$
>Allora:
>$$
> \frac{1}{n^{\alpha}}\geq \frac{1}{n} \iff \sum^{+\infty }_{n=1} \frac{1}{n^{\alpha}}
=+\infty
>$$

>[!warning] Infatti:
>$$
>\begin{align}
>& Sia\ \ S^{(1)}_{n} = \sum^{n}_{k=1} \frac{1}{k} \\
>&\ \ \ \ \ \ \ \ S^{(\alpha)}_{n} = \sum_{k=1}^{n} \frac{1}{k^{n}}
\end{align}$$
>
>$$
>\begin{align}
>& Sia\ \ \alpha \leq 1 \\
>&\text{Allora }\ \frac{1}{k^{\alpha}} \geq \frac{1}{k} \\
>& \text{Allora }\ S^{(\alpha)}_{n} \geq S^{(1)}_{n}\ \ \ \forall n \in \mathbb{N} 
\end{align}$$


**Confronto per i limiti:**

$$
\lim_{ n \to +\infty } S^{(1)}_{n} = +\infty 
$$
per confronto 
$$
\begin{align}
& \boxed{\lim_{ n \to +\infty } S^{(\alpha)}_{n}=+\infty } \\ \\
&\ \ \ \ \ \ \ \ \ \ \ \  \ = \\
&\ \ \ \ \ \ \ \ \ \ \sum^{+\infty }_{n=1} \frac{1}{n^{\alpha}}
\end{align} $$
>[!example] Example:
>1. $\sum^{+\infty}_{n=1}\sqrt{n}=+\infty$
>2. $\sum^{+\infty}_{n=1}- \frac{1}{n^{1/3}}= -\infty$


Caso $\alpha>1$:
- $\sum^{+\infty}_{n=1} \frac{1}{n^{\alpha}} \text{ è convergente}$ (**Stacce**)

**Esempio:**
per esempio $\sum^{+\infty}_{n=1} \frac{1}{n^{2}}$ converge


## Riassuntone serie armoniche

$$
\sum^{+\infty }_{n=1} \frac{1}{n^{\alpha}} = \begin{cases}
\text{Converge} &se\ \ \alpha>1 \\
\text{Diverge} &se\ \ \alpha \leq 1
\end{cases}
$$

---
