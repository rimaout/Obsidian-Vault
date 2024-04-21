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
>1. [[#Definizione]]
>2. [[#Risoluzione di integrali con Primitive]]
>3. [[#Notazioni]]
>4. [[#Primitive Elementari]]

>[!abstract] Related
>- 

---
## Definizione

>[!note] Definizione di Primitiva 1
>Dato $f\in C°([a,b])$
>
>$$
>P\text{ è una primitiva di } f( x )\ \text{ se }\ P^{'}(x) = f( x ) \ \ \ \ \forall x \in (a,b) 
>$$
>

>[!note] Definizione di Primitiva 1
>Dato $f\in C°([a,b])$
>
>$$
>\text{se }P^{'} = f\ \implies (P+c)'=f
>$$
>
>**oss:** $P^{'}_{1}=P_{2}^{'}=f\implies P_{1}-P_{2}=(P_{1}-P_{2})^{'}=0\implies P_{1}-P_{2}=c$

>[!warning] Anti derivata
>Le primitive vengono chiamate anche anti [[Derivate|derivate]], perché compiono il "calcolo" inverso di una derivata

---
## Risoluzione di integrali con Primitive

>[!info]
>Dato $f\in C°([a,b])$
>
>$$
>\int^{b}_{a} f( x ) \ dx = \big[F( x )\big]_{a}^{b} = F(b)-f(a)
>$$
>
>$F(x)$ è una **primitiva** di $f( x )$ se:
>- $F(x)$ è derivabile
>- $F^{'}(x) = f(c)\ \ \forall x \in (a,b)$
>
>Ovvero se ogni funzione continua nel intervallo $[a,b]$ ammette derivate

---
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

>[!warning] oss
>Sono le inverse di una derivata
