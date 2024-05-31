---
created: 2023-12-08
type: Uni Note
class:
  - "[[Calcolo Differenziale (class)]]"
academic year: 2023/2024
related:
  - "[[Derivate]]"
  - "[[Derivata prima]]"
  - "[[Funzioni Monotone]]"
completed: true
updated: 2024-05-27T13:29
---
---
## Index
1. [[#Enunciato]]
2. [[#Conseguenze]]

---
## Enunciato
- Sia $f:[a,b]\to \mathbb{R}$
	- [[Funzioni Continue|Continua]] in $[a,b]$
	- [[Funzione derivabile|Derivabile]] in $[a,b]$

- Allora $\exists c \in (a,b)$:
	$$f^{'}(c)=\frac{f(b)-f(a)}{b-a}$$
	![[IMG_E69D8D6A99C0-1.jpeg|800]]

---
## Conseguenze (crescente i un intervallo)

>[!def] Definitions:
>- **Crescente:**
> 	- $f(x)$ è crescente se $\textcolor{orange}{\frac{f(x)-f(y)}{x-y}\geq 0}\ \ \ \ \ \ \  \forall x\not=y\in[a,b]$ 
>- **Decrescente:**
> 	- $f(x)$ è decrescente se $\textcolor{orange}{\frac{f(x)-f(y)}{x-y}\leq 0}\ \ \ \ \ \ \  \forall x\not=y\in[a,b]$  

**Sbagliato inverire y con x e vice versa**
![[IMG_46899E0EAB77-1.jpeg|700]]

>[!warning] Oss:
>- Se $f$ è *crescente* allora è derivabile $\iff f^{'}(x)\geq 0$
>- Se $f$ è *decrescente* allora è derivabile $\iff f^{'}(x)\leq 0$

---
## Conseguenze esiste punto con stesso coefficiente angolare di f'(c)

Esiste sicuramente un altro punto $x_{0}$ in cui la funzione ($f(x_{0})$) a come coefficiente angolare $\frac{f(b)-f(a)}{b-a}$

>[!warning] Oss:
>$a<x_{0}<b$

---