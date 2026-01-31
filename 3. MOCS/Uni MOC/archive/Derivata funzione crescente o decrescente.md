---
created: 2023-12-28
type: Uni Note
class:
  - "[[Calcolo Differenziale (class)]]"
academic year: 2023/2024
related:
  - "[[Teorema di Lagrange]]"
  - "[[Funzioni Monotone]]"
completed: true
updated: 2026-01-31T13:32
---
---

**Leggi:** [[Teorema di Lagrange]]

>[!example] Example:
> $$
> f(x) = \begin{cases}
 5x^{2} & \text{if } x\geq 0 \\
 6-3x^{2} & \text{if x < 0}
>
>\end{cases}$$
>**1)** $f(x)$ crescente su $(0,+\infty)?$
>**2)** $f(x)$ decrescente su $(-\infty, 0)?$
>**3)** $f(x)$ crescente su $\mathbb{R}$?

>[!example] **1)** $f(x)$ crescente su $(0,+\infty)?$
>*Metodo:*
>-  Fare $f(x)'$
>	- Se $f(x)'>0$   $\ \forall x \in (0,+\infty)$ $\implies$ $f(x)$ crescente su $(0,+\infty)$ 
>	- Se $f(x)'<0$   $\ \forall x \in (0,+\infty)$ $\implies$ $f(x)$ decrescente su $(0,+\infty)$
> 
>*Calcoli:*
>- $f(x) = 6-3x^{2}$ e $f(x)' = 6-6x$ 
>- $6-6x$ e sempre positivo $\forall x \in (-\infty,0)$
>
>*Quindi:* $f(x)$ è crescente su $(-\infty,0)$

>[!example] **2)** $f(x)$ decrescente su $(-\infty, 0)?$
>*Metodo:*
>-  Fare $f(x)'$
>	- Se $f(x)'>0$   $\ \forall x \in (0,+\infty)$ $\implies$ $f(x)$ crescente su $(-\infty,0)$ 
>	- Se $f(x)'<0$   $\ \forall x \in (0,+\infty)$ $\implies$ $f(x)$ decrescente su $(-\infty, 0)$
> 
>*Calcoli:*
>- $f(x) = 5x^{2}$ e $f(x)' = 10x$ 
>- $10x$ e sempre positivo $\forall x \in (0, +\infty)$
>
>*Quindi:* $f(x)$ è crescente su $(0, +\infty)$

>[!example] **3)** $f(x)$ crescente su $\mathbb{R}$
>*Metodo:*
>- Osservare $f(x)$ si comporta:
>	- $\forall  x \in(-\infty,0)$
>	- $\forall  x \in (0.+\infty)$
>	- $x = 0$ (unico punto che non abbiamo studiato)
>
>*Calcoli:*
>- $\forall  x \in(-\infty,0)$,  $f(x)$ è sempre crescente *(visto in esempio 1)*
>- $\forall  x \in (0.+\infty)$,  $f(x)$ è sempre crescente *(visto in esempio 2)*
>- $x = 0$:
>	- $\lim_{ x \to 0^{+} }5x^{2} = 5\cdot 0 = 0$ 
>	- $\lim_{ x \to 0^{-} }6-3x^{2}=6-3\cdot 0 = 6$
>	
>*Quindi:* $f(x)$ non è crescente su tutto $\mathbb{R}$ 
>![[Pasted image 20231228162458.png|400]]

