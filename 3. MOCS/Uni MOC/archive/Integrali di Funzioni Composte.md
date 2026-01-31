---
created: 2024-04-21
type: Uni Note
class:
  - "[[Calcolo Integrale (class)]]"
academic year: 2023/2024
related:
  - "[[Primitive]]"
  - "[[Integrali]]"
  - "[[Primitive Elementari]]"
completed: true
updated: 2026-01-31T13:32
---
---

>[!abstract] Index
>1. [[#Definizione]]
>2. [[#Primitive Elementari Generalizzate]]
>3. [[#Esempi]]

>[!abstract] Related
>- [[Calcolo Integrale (class)]]
>- [[Primitive Elementari]]
>- [[Integrali]]

---
## Definizione

>[!info] Formula
>$$
>\int f\big(g(x)\big)\cdot g^{'}(x) \ dx = F\big(g(x)\big)+c
>$$

>[!warning] Deriva da
>
>$$
>\Big[f\big(g(x)\big)\Big]' = f\big(g(x)\big)\cdot g'(x)
>$$

---
## Primitive di funzioni composte elementari

| Primitive Elementare                                         | Generalizzazione                                                       |
| ------------------------------------------------------------ | ---------------------------------------------------------------------- |
| $\int \cos x \ dx$ = $\sin x +c$                             | $\int f'( x ) \cos \big[f( x )\big] \ dx$ = $\sin [f( x )]+c$          |
| $\int \sin x  \ dx$ = $-\cos x+c$                            | $\int f'( \big[f( x )\big] ) \sin x  \ dx = -\cos [f( x )]+c$          |
| $\int e^{x} \ dx$ = $e^{x}+c$                                | $\int f'( x )\ e^{f( x )} e^{f( x )} \ dx +c$                          |
| $\int a^{x} \ dx$                                            |                                                                        |
| $\int x^{n} \ dx$ = $\frac{x^{n+1}}{n+1}+c$  con $n \not=-1$ | $\int f'( x )\ \big[f( x )\big]^{n} \ dx \frac{[f( x )]^{n+1}}{n+1}+c$ |
| $\int \frac{1}{x} \ dx$ = $\ln \mid x\mid +\ c$              | $\int f'( x )\ \frac{1}{\big[f( x )\big]} \ln \mid [f( x )]\mid+\ c$   |
| $\int \frac{1}{1+x^{2}} \ dx$                                |                                                                        |

>[!tip]- Imagine (più leggibile)
>![[Pasted image 20240421190728.png|900]]

>[!danger] Derivano dalla formula:
> $\int f\big(g(x)\big)\cdot g^{'}(x) \ dx = F\big(g(x)\big)+c$

---
## Esempi

>[!example] Esempio 1
>![[Pasted image 20240421181129.png|500]]

>[!example] Esempio 2
>![[Pasted image 20240421181612.png|500]]

>[!example] Esempio 3
>![[Pasted image 20240421182553.png|700]]
>
>**oss:** Usata formula $x^{n} = \frac{x^{n+1}}{n+1}$ con $x=n^{2}+1$ e $n=2014$

>[!example] Esempio 4
>![[Pasted image 20240421184821.png|700]]

---