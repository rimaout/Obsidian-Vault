---
created: 2023-12-09
type: Uni Note
class:
  - "[[Calcolo Differenziale (class)]]"
academic year: 2023/2024
related:
  - "[[Limiti]]"
  - "[[Formula di Taylor]]"
completed: true
updated: 2026-01-31T13:32
---

>[!abstract] Index
>1. [[#Definizione (libro)]]
>2. [[#Definizione (Prof. Orsina)]]
>3. [[#Proprietà]]

>[!abstract] Related
>- [[Limiti]]
>- [[Calcolo Differenziale (class)]]

---
## Definizione (libro)

$$
\begin{align}
& - \ \ \text{Siano f(x) e g(x) due funzioni definite in un introno di }x_{0}, \\ 
& \ \ \ \ \ \  \ \text{dove }x_{0} \in \mathbb{R} \\ \\
& - \ \ se \ \lim_{ x \to x_{0} }\frac{f(x)}{g(x)}=0\ \ \ \ allora: \\ \\
&- \ \ f(x) = o(g(x))\ \ per\ \ x\to x_{0}  
\end{align}
$$

>[!warning] Intuitivamente
>- *f(x) è un o piccolo di di g(x)*  per $x\to x_{0}$ è equivalente a dire che:
>- *f(x) è infinitamente più piccola, rispetto a g(x)*, quando $x\to x_{0}$

---
## Definizione (Prof. Orsina)

>[!Def] Def: O piccolo 
> Si dice $o(h^n)$ ($n\in\mathbb{N}$) \[si legge o piccolo di h\] una qualsiasi quantità tale che:
> $$\lim_{ h \to o } \frac{o(h)}{h}= 0 $$
^ae71f1

>[!example] Esempi
>1. $h^{2}$ *è* $o(h)$
>	- dim: $\lim_{ h \to 0 } \frac{h^{2}}{h}=\lim_{ h \to 0}h=0$
>2. $h^{2}$ *non è* $o(h^{2})$
>	- dim: $\lim_{ h \to 0 } \frac{h^{2}}{h^{2}}=1$
>3. $\sin(h^{3})$ *é* $o(h^{2})$
>	- dim: $\lim_{ h \to 0 } \frac{\sin(h^{3})}{h^{2}}=\lim_{ h \to 0 }h=0$
>4. $1-\cos(h)$ *é* $o(h)$
>	- dim: $\lim_{ h \to 0 } \frac{1-\cos(h)}{h}=0$
>5. $h^{3}+3h^{2}$ *non é* $o(h^{2})$
>	- dim: $\lim_{ h \to 0 } \frac{h^{3}+3h^{2}}{h^{2}}=\lim_{ h \to 0 }h+3=3$
>6. $h^{3}+3h^{2}$ *é* $o(h)$
>	- dim: $\lim_{ h \to 0 } \frac{h^{3}+3h^{2}}{h^{2}}=\lim_{ h \to 0 }h^{2}+3h=0$
>	 
^04b53d

---
## Proprietà

>[!note] Proprietà
>- $h^{k}\cdot o(h^{n})=o(h^{n+k})$
>- $o(h^{k})\cdot o(h^{n})=o(h^{n+k})$
>- $o(h^{n})\pm o(h^{n})=o(h^{n})$
>- $M\cdot o(h^{n})=o(h^{n})\ \ \ \ M\in\mathbb{R}$
^8e2aa2

>[!example] Esempio 1
>$x^{3}=o(x^{2})$ vero o falso ?
>- una quantità è $o(X^{2})$ se, dicidendola per $x^{2}$, e facendola tendere $x$ a zero, il limite vale zero
>$$\lim_{ x \to o } \frac{x^{3}}{x^{2}}=\lim_{ x \to 0 } x=0$$

>[!example] Esempio 2
>$x^{3}=o(x^{3})?$
>
>$$
>\lim_{ x \to 0 } =\lim_{ x \to 0 }
>$$ 
