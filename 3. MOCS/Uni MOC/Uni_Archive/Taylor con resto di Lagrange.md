---
created: 2024-04-08
type: Uni Note
class:
  - "[[Calcolo Integrale (class)]]"
academic year: 2023/2024
related:
  - "[[Serie di Taylor]]"
completed: true
updated: 2024-05-27T13:29
---
---

>[!info] Index
>1. [[#Formula di Taylor con resto di Lagrange (Teorema)]]
>2. [[#Significato]]

---
## Formula di Taylor con resto di Lagrange (Teorema)
Nelle ipotesi della formula di Taylor, e con l'ulteriore ipotesi aggiuntiva che esista la derivata $f^{(n)}(x_{0})$ allora esiste un punto $c \in (a,b)$ tale che:

$$
\begin{align*}
& T_{n}(f(x),\ \ x_{0})=\textcolor{orange}{\sum_{k=0}^{n-1} \frac{f^{(k)}(x_{0})}{k!}(x-x_{0})^{k}} + \textcolor{lightgreen}{\frac{f^{(n)}(c)}{n!}(x-x_{0})^{n}} \\ \\
& \ \ \ \ \ \ \ \ \ \ \ - \textcolor{orange}{\text{Polinomio di grado}\leq n-1} \\ 
& \ \ \ \ \ \ \ \ \ \ \ - \textcolor{lightgreen}{\text{Resto di Lagrange}} \\ \\
& \text{Dove:} \\
& \ \ \ \ \ \ \ -\ f(x)\ \text{è la funzione da approssimare} \\
& \ \ \ \ \ \ \ -\ n\ \text{è il grado di approssimazione} \\
& \ \ \ \ \ \ \ -\ x_{0}\in(a,\ b)\ \text{è il punto in cui approssimare (centro dello sviluppo)} \\ \\
& \text{Prerequisiti:} \\
& \ \ \ \ \ \ \ -\ f(x)\ \text{è definita in un certo intervallo }(a,\ b)\\
& \ \ \ \ \ \ \ -\ c \in (a,\ b)\\
& \ \ \ \ \ \ \ -\ f(x)\ \text{è derivabile }n-1\text{ volte nell'intervallo}\\
& \ \ \ \ \ \ \ -\ \text{esiste la derivata n-esima in }x_{0} \\ \\ \\
\end{align*}
$$

---
## Significato

Il resto di Lagrange, a differenza di quello di [[Taylor con resto di Peano|Peano]], fornisce informazioni **quantitative** sul resto.

Anche in questo caso non sappiamo né ci interessa capire quale sia il punto c per cui vale l'asserto. È sufficiente sapere che c'è e che la valutazione della derivata n-esima in tale punto conduce ad una rappresentazione esatta.

