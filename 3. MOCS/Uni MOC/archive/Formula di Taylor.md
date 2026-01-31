---
created: 2023-12-29
type: Uni Note
class:
  - "[[Calcolo Differenziale (class)]]"
academic year: 2023/2024
related:
  - "[[Derivate]]"
  - "[[Limiti]]"
  - "[[Sviluppi di Taylor centrati in 0]]"
completed: true
updated: 2026-01-31T13:32
---
---

>[!info] Index
>1. [[#Definizione]]
>2. [[#Formula Sviluppo serie di Taylor]]
>3. [[#Sviluppo di Taylor con resto]]

---
## Definizione

Lo sviluppo in serie di Taylor di una funzione in un punto, se esiste, permette di esprimere la funzione nell'intorno del punto come un polinomio con infiniti termini. 

>[!note]
>Arrestando lo sviluppo di Taylor ad un certo ordine consente di **approssimare**, almeno **localmente** (nel punto $x_{0}$, tutte le funzioni sufficientemente regolari con dei polinomi.

---
## Formula Sviluppo serie di Taylor

$$
\begin{align*}
& T_{n}(f(x),\ \ x_{0})=\textcolor{orange}{\sum_{k=0}^{n-1} \frac{f^{k}(x_{0})}{k!}(x-x_{0})^{k}}+\textcolor{lightgreen}{R_{n}(x)} \\ \\
& \ \ \ \ \ \ \ \ \ \ \ - \textcolor{orange}{\text{Polinomio di grado}\leq n-1} \\ 
& \ \ \ \ \ \ \ \ \ \ \ - \textcolor{lightgreen}{\text{Resto di ordine n}} \\ \\
& \text{Dove:} \\
& \ \ \ \ \ \ \ -\ f(x)\ \text{è la funzione da approssimare} \\
& \ \ \ \ \ \ \ -\ n\ \text{è il grado di approssimazione} \\
& \ \ \ \ \ \ \ -\ x_{0}\in(a,\ b)\ \text{è il punto in cui approssimare (centro dello sviluppo)} \\ \\
& \text{Prerequisiti:} \\
& \ \ \ \ \ \ \ -\ f(x)\ \text{è definita in un certo intervallo }(a,\ b)\\
& \ \ \ \ \ \ \ -\ f(x)\ \text{è derivabile }n-1\text{ volte nell'intervallo}\\
& \ \ \ \ \ \ \ -\ \text{esiste la derivata n-esima in }x_{0} \\ \\
\end{align*}
$$

>[!tip] Sviluppo di una funzione
>$$
>T_{n}(f(x), x_{0})= f(x_{0}) + f'(x_{0})(x-x_{0}) + \frac{f''(x_{0})}{2}(x-x_{0})^{2}+ \frac{f'''(x_{0})}{6}(x-x_{0})^{3}+\dots+\frac{f^{k}(x_{0})}{n!}(x-x_{0})^{n}
>$$

---
## Sviluppo di Taylor con resto

Polinomio di Taylor abbiamo detto che **approssima** la funzione, ma se aggiungiamo un termine complementare (detto resto) possiamo ottenere la funzione stessa.

>[!note]
>Arrestando lo sviluppo di Taylor ad un certo ordine è possibile esprimere i restanti termini sotto forma di resto.

$$
\begin{align}
& T_{n}(f(x),\ \ x_{0})=\textcolor{orange}{\sum_{k=0}^{n-1} \frac{f^{k}(x_{0})}{k!}(x-x_{0})^{k}}+\textcolor{lightgreen}{R_{n}(x)} \\ \\
& \ \ \ \ \ \ \ \ \ \ \ - \textcolor{orange}{\text{Polinomio di grado}\leq n-1} \\ 
& \ \ \ \ \ \ \ \ \ \ \ - \textcolor{lightgreen}{\text{Resto di ordine n}} \\ \\
\end{align}
$$

**Esistono due tipi di resto:**
- [[Taylor con resto di Peano]]
- [[Taylor con resto di Lagrange]]

---
