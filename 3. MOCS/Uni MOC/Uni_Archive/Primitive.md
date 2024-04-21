---
Created: 2024-04-20
Type: Uni Note
Class:
  - "[[Calcolo Integrale (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Integrali]]"
Completed: false
---
---

>[!abstract] Index
>1. 

>[!abstract] Related
>- 

---
## Definizione

se $f\in C°([a,b])$

$$
\int^{b}_{a} f( x ) \ dx = \big[F( x )\big]_{a}^{b} = F(b)-f(a)
$$
>[!note] Definizione di primitiva
>$F(x)$ è una **primitiva** di $f( x )$ se:
>- $F(x)$ è derivabile
>- $F^{'}(x) = f(c)\ \ \forall x \in (a,b)$
>
>Ovvero ogni funzione continua nel intervallo $[a,b]$ ammette derivate

## Notazioni

>[!warning] Funzione continua nell'intervallo
>
>$$
>\begin{align}
>& f\in C°([a,b]) \implies \text{[a,b]} \\ \\
>&\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \text{o} \\ \\
>&\ \ \ \ \ \ \ \ \ \ f:[a,b] \to \mathbb{R}
>\end{align}
>$$

>[!warning] Generica primitiva di f(x)
>
>$$
>\int f( x ) \ dx
>$$

---
## Primitive Elementari

| $f(x)$              | F(x)                                         |
| ------------------- | -------------------------------------------- |
| $\cos x$            | $\sin x$                                     |
| $\sin x$            | $-\cos x$                                    |
| $e^{x}$             | $e^{x}$                                      |
| $a^{x}$             | $\frac{a^{x}}{\ln a}$                        |
| $x^{n}$             | $\frac{x^{n+1}}{n+1}\ \ \ \forall n \not=-1$ |
| $1/x$               | $\ln \mid x\mid$                             |
| $\frac{1}{1+x^{2}}$ | $\text{arctg}\ x$                            |
