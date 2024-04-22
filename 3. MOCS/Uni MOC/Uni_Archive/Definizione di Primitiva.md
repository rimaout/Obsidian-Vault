---
Created: 2024-04-21
Type: Uni Note
Class:
  - "[[Calcolo Integrale (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Integrali]]"
  - "[[Primitive]]"
Completed: false
---
---

>[!abstract] Index
>1. [[#Definizione]]
>2. [[#Risoluzione di integrali con Primitive]]
>3. [[#Notazioni]]

>[!abstract] Related
>- [[Integrali]]
>- [[Calcolo Integrale (class)]]

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
>\int f( x ) \ dx = \{F:F'=f\}
>$$
>
>ovvero insieme delle primitive



---