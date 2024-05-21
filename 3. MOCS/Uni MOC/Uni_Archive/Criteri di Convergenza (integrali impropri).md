---
Created: 2024-05-20
Type: Uni Note
Class:
  - "[[Calcolo Integrale (class)]]"
Academic Year: 2023/2024
Related: 
Completed: false
---
---

>[!abstract] Index
>1. [[#Criterio Confronto Asintotico]]
>2. [[#Criterio Confronto]]
>3. [[#^37ec46|Esempi]] 

>[!abstract] Related
>- [[Integrali]]
>- [[Integrali Impropri]]
>- [[Calcolo Integrale (class)]]

---
## Criterio Confronto Asintotico 

>[!info] Zona di Integrazione Illimitata
>Siano $f,g:[a,+\infty)\to \mathbb{R}$ due funzioni continue e positive:
>$$
>\lim_{ x \to x_{0} } \frac{f(x)}{g(x)} = \ell \implies \int^{+\infty }_{a} f( x ) \ dx \sim \int^{+\infty }_{a} g(x)\ dx
>$$
>Quindi sappiamo che:
>- Se $\int^{+\infty}_{a}  g(x)\, dx$ **converge**, allora $\int^{+\infty}_{a} f(x)\, dx$ **converge**
>- Se $\int^{+\infty}_{a}  g(x)\, dx$ **diverge**, allora $\int^{+\infty}_{a} f(x)\, dx$ **diverge**
>
>**oss:** analogo al [[Criterio del confronto asintotico (Serie)]]

>[!info] Funzione Illimitata
>Siano $f(x)$ e $g(x)$ due funzioni, continue e positive, tali che in $x_{0}$ vi sia un punto illimitato e $\ell \in (0, +\infty)$, allora:
>$$
>\lim_{ x \to x_{0} } \frac{f(x)}{g(x)} = \ell \implies \int^{x_{0}}_{a} f( x ) \ dx \sim \int^{x_{0} }_{a} g(x)\ dx
>$$
>
>Quindi sappiamo che:
>- Se $\int^{x_{0}}_{a}  g(x)\, dx$ **converge**, allora $\int^{x_{0}}_{a} f(x)\, dx$ **converge**
>- Se $\int^{x_{0}}_{a}  g(x)\, dx$ **diverge**, allora $\int^{x_{0}}_{a} f(x)\, dx$ **diverge**
>
>**oss:** analogo al [[Criterio del confronto asintotico (Serie)]]

---
## Criterio Confronto

>[!info] Zona di Integrazione Illimitata
>Siano $f,g:[a,+\infty)\to \mathbb{R}$ due funzioni, se:
>$$
>0\leq f(x)\leq g(x)\ \text{in } [a,+\infty)
>$$
>
>Allora sappiamo che:
>- Se $\int^{+\infty}_{a}  g(x)\, dx$ **converge**, allora $\int^{+\infty}_{a} f(x)\, dx$ **converge**
>- Se $\int^{+\infty}_{a} f(x)\, dx$ **diverge**, allora $\int^{+\infty}_{a} g(x)\, dx$ **diverge**
>
>**oss:** analogo al [[Criterio del confronto (Gauss - Serie)]]

>[!info] Funzione Illimitata
>Siano $f(x)$ e $g(x)$ due funzioni tali che in $x_{0}$ vi sia un punto illimitato, se:
>
>$$
>0\leq f(x)\leq g(x)\ \text{in } [a,x_{0})
>$$
>
>Allora sappiamo che:
>- Se $\int^{x_{0}}_{a}  g(x)\, dx$ **converge**, allora $\int^{x_{0}}_{a} f(x)\, dx$ **converge**
>- Se $\int^{x_{0}}_{a} f(x)\, dx$ **diverge**, allora $\int^{x_{0}}_{a} g(x)\, dx$ **diverge**
>
>**oss:** analogo al [[Criterio del confronto (Gauss - Serie)]]

---
## Criterio Convergenza Assoluta

>[!info] Zona di Integrazione Illimitata

>[!info] Funzione Illimitata
>Sia $f(x)$ una funzione tale che in $x_{0}$ vi sia un punto illimitato, allora:
>
>$$
>\int^{x_{0}}_{a} \big\vert f( x)\big\vert \ dx < +\infty \implies  >\int^{x_{0}}_{a} f( x) \ dx < +\infty 
>$$
>
>**oss:** analogo al [[Criterio della convergenza assoluta (Serie)]]

---
![[Esercizi Integrali Impropri#Esercizi con criteri di convergenza]] ^37ec46