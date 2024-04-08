---
Created: 2023-12-29
Type: Uni Note
Class:
  - "[[Calcolo Differenziale (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Derivate]]"
  - "[[Limiti]]"
  - "[[Sviluppi di Taylor centrati in 0]]"
Completed: true
---
---
>[!info]


---
## Definizione

Lo sviluppo in serie di Taylor di una funzione in un punto, se esiste, permette di esprimere la funzione nell'intorno del punto come un polinomio con infiniti termini. 

Arrestando lo sviluppo di Taylor ad un certo ordine è possibile esprimere i restanti termini sotto forma di resto.

La formula di Taylor consente di approssimare, almeno localmente (nel punto $x_{0}$, tutte le funzioni sufficientemente regolari con dei polinomi.

---
## Introduzione

Vogliamo determinare un polinomio $P$​ di grado $n$ che calcolato nel punto $a$ sia uguale alla funzione calcolata nel punto a e che la derivata prima del polinomio calcolata nel punto a sia uguale alla derivata della funzione calcolata nel punto a. Così via per tutte le derivate, quindi:

$$
P^{(n)}(a)=f^{(n)}(a)
$$

---

$$
\begin{align}
& T_{n}(f(x),\ \ x_{0})=\textcolor{orange}{\sum_{k=0}^{n-1} \frac{f^{k}(x_{0})}{k!}(x-x_{0})^{k}}+\textcolor{lightgreen}{o[(x-x_{0})^{n}]} \\ \\
& \ \ \ \ \ \ \ \ \ \ \ - \textcolor{orange}{\text{polinomio di grado}\leq n} \\ 
& \ \ \ \ \ \ \ \ \ \ \ - \textcolor{lightgreen}{\text{infinitesimo di grado superiore a n (Resto di Peano)}} \\ \\
& \text{Dove:} \\
& \ \ \ \ \ \ \ -\ f(x)\ \text{è la funzione da approssimare} \\
& \ \ \ \ \ \ \ -\ n\ \text{è il grado di approssimazione} \\
& \ \ \ \ \ \ \ -\ x_{0}\ \text{è il punto in cui approssimare} \\ \\
& \text{Prerequisiti:} \\
& \ \ \ \ \ \ \ -\ f(x)\ \text{è definita in un certo intervallo }(-\delta, \delta)\ \ \ \forall \delta>0 \\
& \ \ \ \ \ \ \ -\ f(x)\ \text{è derivabile }n-1\text{ volte nell'intervallo}\\
& \ \ \ \ \ \ \ -\ \text{esiste la derivata n-esima in }x_{0} \\ \\
\end{align}
$$

---
## Sviluppo di f(x)
$$
T_{k}((x), x_{0})= f(x_{0}) + f'(x_{0})(x-x_{0}) + \frac{f''(x_{0})}{2}(x-x_{0})^{2}+ \frac{f'''(x_{0})}{6}(x-x_{0})^{3}+\dots+\frac{f^{k}(x_{0})}{k!}(x-x_{0})^{k}
$$
---
## Conseguenze

>[!warning] Teorema:
> Polinomio di tailor di ordine n di un polinomio di grado n è il polinomio stesso

---