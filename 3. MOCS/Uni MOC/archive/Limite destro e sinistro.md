---
created: 2023-11-17
type: Uni Note
class:
  - "[[Derivate]]"
academic year: 2023/2024
related:
  - "[[Limiti]]"
  - "[[Numeri Reali]]"
completed: true
updated: 2026-01-31T13:32
---
>[!abstract] Index
>1. [[#Limite destro]]
>2. [[#Limite sinistro]]
>3. [[#Limite bilatero]]

>[!abstract] Related
>- [[Limiti]]
>- [[Calcolo Differenziale (class)]]

---
## Limite destro
$$
\lim_{ {n \to x_{0}}^{+} } f(x)=L
$$

>[!note] Definizione
>$$
>\forall \epsilon>0\ \ \exists \delta_{\epsilon}>0:\ \ \ \ \ \ 0<x-x_{0}\leq \delta_{\epsilon}\implies|f(x)-L|\leq \epsilon
>$$

---
## Limite sinistro

$$
\lim_{ {n \to x_{0}}^{-}} f(x)=M
$$

>[!note] Definizione
>$$
>\forall \epsilon>0\ \ \exists \delta_{\epsilon}>0:\ \ \ \ \ \ 0<x_{0}-x<\delta_{\epsilon}\implies|f(x)-M|\leq \epsilon
>$$

---
## Limite bilatero
Se $f$ è una funzione definita nell'intorno $x_{0}\in\mathbb{R}$ essa ha limite $\ell\in\mathbb{R}\cup \{ \pm \infty \}$ per $x\to x_{0}$ se e solo se:
- Il limite destro e il limite sinistro fi $f$ in $x_{0}$ esistono e sono uguali ad $\ell$ (limite di $f$)
- $\underset{ n \to \infty }{ \lim }f(x) = \ell \iff f \underset{ n \to {\infty}^{-} }{ \lim }f(x)=\underset{ n \to {\infty}^{+} }{ \lim }f(x)=\ell$

>[!note] Limite finito
> per $x\to x_{0}$ devono essere finiti e uguali sia il limite sinistro e che il limite destro

>[!note] Limite infinito
>per $x\to x_{0}$ devono essere infiniti e di segno concorde sia il limite sinistro e che il limite destro