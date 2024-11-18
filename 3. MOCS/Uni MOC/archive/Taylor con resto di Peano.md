---
created: 2024-04-08
type: Uni Note
class:
  - "[[Calcolo Differenziale (class)]]"
academic year: 2023/2024
related:
  - "[[Serie di Taylor]]"
completed: true
updated: 2024-05-27T13:29
---
---

>[!info] Index
>1. [[#Formula di Taylor con resto di Peano (Teorema)]]
>2. [[#Significato]]

---
## Formula di Taylor con resto di Peano (Teorema)

Nelle ipotesi della formula di Taylor, e con l'ipotesi aggiuntiva che esista $f^{(n)}(x_{0})$, vale la formula:

$$
\begin{align*}
& T_{n}(f(x),\ \ x_{0})=\textcolor{orange}{\sum_{k=0}^{n} \frac{f^{k}(x_{0})}{k!}(x-x_{0})^{k}}+\textcolor{lightgreen}{o[(x-x_{0})^{n}]} \\ \\
& \ \ \ \ \ \ \ \ \ \ \ - \textcolor{orange}{\text{polinomio di grado}\leq n} \\ 
& \ \ \ \ \ \ \ \ \ \ \ - \textcolor{lightgreen}{\text{infinitesimo di grado superiore a n (Resto di Peano)}} \\ \\
& \text{Dove:} \\
& \ \ \ \ \ \ \ -\ f(x)\ \text{è la funzione da approssimare} \\
& \ \ \ \ \ \ \ -\ n\ \text{è il grado di approssimazione} \\
& \ \ \ \ \ \ \ -\ x_{0}\ \text{è il punto in cui approssimare (centro dello sviluppo)} \\ \\
& \text{Prerequisiti:} \\
& \ \ \ \ \ \ \ -\ f(x)\ \text{è definita in un certo intervallo }(a,\ b)\\
& \ \ \ \ \ \ \ -\ f(x)\ \text{è derivabile }n-1\text{ volte nell'intervallo}\\
& \ \ \ \ \ \ \ -\ \text{esiste la derivata n-esima in }x_{0} \\ \\
\end{align*}
$$

>[!warning] Nota
>Il termine$o[(x-x_{0})^{n}]$, dove $o(\cdot)$ indica l'[[o piccolo di h|o-piccolo]], è dato da una qualsiasi funzione $g(x)$ tale che:
>
>$$
>\lim_{ x \to x_{0} } \frac{g(x)}{(x-x_{0})^{n}} = 0
>$$

---
## Significato

- Il resto di Peano fornisce informazioni di tipo **qualitativo**. 
- È cruciale capire sin da subito che non importa sapere quale sia la funzione precisa che porta all'uguaglianza, mentre è importante capire qual è il comportamento qualitativo della funzione Rn().

Il termine $o[(x-x_{0})^{n}]$ individua una funzione qualsiasi che nell'intorno di $x_{0}$ tende a zero più velocemente di $(x-x_{0})^{n}$.
