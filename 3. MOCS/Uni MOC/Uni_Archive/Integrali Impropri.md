---
Created: 2024-05-13
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
>2. [[#Criteri di convergenza]]
>	- [[#^d2df11|Criterio Confronto Asintotico]]
>	- [[#^0e4af8|Criterio Confronto]]
>	- [[#^d2d302|Criterio Convergenza Assoluta]]

>[!abstract] Related
>- [[Integrali]]
>- [[Calcolo Integrale (class)]]

---
## Definizione 

>[!info] Integrale improprio
>Sia $f(x)$ una funzione di **discontinuità illimitata** nel punto $x=b$, allora:
>
>$$
>\int^{b}_{a} f(x) \ dx = \text{ Non Integrabile Secondo Rienmann}
>$$
>
>Allora, $f(x)$ si dice **integrabile in senso improprio**  in $[a,\, b]$ se l'integrale per $[a, \, b-\epsilon ]$ doce $\epsilon \to 0^{+}$ ammette limite finito:
>
>$$
>\lim_{ \epsilon \to 0^{+} } \int^{b-\epsilon}_{a} f(x) \ dx = \lim_{ \epsilon \to 0^{+} } F(x) \Bigg\vert^{b-\epsilon}_{a} = \ell
>$$
>
>Dove:
>- $\ell$ è un numero finito 
>- $F(x)$ è una [[Primitive|primitiva]] di $f(x)$

---
## Criteri di convergenza 

- [[Analogia tra Serie Numeriche ed Integrali Impropri]]  🔴

>[!info] Criterio del Confronto Asintotico
>Siano $f(x)$ e $g(x)$ due funzioni tali che in $x_{0}$ vi sia un punto illimitato e $\ell \in (0, +\infty)$, allora:
>$$
>\lim_{ x \to x_{0} } \frac{f(x)}{g(x)} = \ell \implies \int^{x_{0}}_{a} f( x ) \ dx \approx \int^{x_{0} }_{a} g(x)\ dx
>$$
>
>Allora sappiamo che:
>- Se $g(x)$ **converge**, allora $f(x)$ **converge**
>- Se $g(x)$ **diverge**, allora $f(x)$ **diverge**
>
>**oss:** analogo al [[Criterio del confronto asintotico (Serie)]]

^d2df11

>[!info] Criterio del Confronto
>Siano $f(x)$ e $g(x)$ due funzioni tali che in $x_{0}$ vi sia un punto illimitato, allora:
>
>$$
>0\leq \int^{x_{0}}_{a} f(x) \ dx \leq \int^{x_{0}}_{a} g(x)\ dx
>$$
>
>Allora sappiamo che:
>- Se $g(x)$ **converge**, allora $f(x)$ **converge**
>- Se $f(x)$ **diverge**, allora $g(x)$ **diverge**
>
>**oss:** analogo al [[Criterio del confronto (Gauss - Serie)]]

^0e4af8

>[!info] Criterio Convergenza Assoluta
>Sia $f(x)$ una funzione tale che in $x_{0}$ vi sia un punto illimitato, allora:
>
>$$
>\int^{x_{0}}_{a} \big\vert f( x)\big\vert \ dx < +\infty \implies  >\int^{x_{0}}_{a} f( x) \ dx < +\infty 
>$$
>
>**oss:** analogo al [[Criterio della convergenza assoluta (Serie)]]

^d2d302

---

