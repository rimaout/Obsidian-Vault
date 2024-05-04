---
Created: 2024-05-02
Type: Uni Note
Class:
  - "[[Calcolo Integrale (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Primitive]]"
  - "[[Integrali]]"
Completed: false
---
---

>[!abstract] Index
>1. [[#Primitive Elementari Generalizzate]]

>[!abstract] Related
>- [[Primitive]]
>- [[Integrali]]
>- [[Calcolo Integrale (class)]]

---
## Primitive Elementari Generalizzate 

>[!info] Generalizzate per [[Primitive di Derivate di Funzioni Composte]]

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

>[!danger] Derivano dalla formula $\int f\big(g(x)\big)\cdot g^{'}(x) \ dx = F\big(g(x)\big)+c$

---