---
Created: 2024-03-04
Type: Uni Note
Class:
  - "[[Calcolo Integrale (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Serie Numeriche]]"
Completed: true
---
---

>[!info] Index
>1. [[#Serie Armonica]]
>2. [[#Serie Armonica Generalizzata]]
>3. [[#Serie Armonica a Segni Alterni]]
>4. [[#Serie Armonica Modificata]]

---
## Serie Armonica

>[!note] Definition
>Si dice serie armonica la serie:
>$$
>\sum^{+\infty }_{n=1} \frac{1}{n} = +\infty 
>$$

- È una [[serie a termini positivi]] e diverge sempre positivamente indipendentemente dal valore di $n$.
- Quindi è non può essere una serie irregolare (indeterminata)
---
## Serie Armonica Generalizzata 

>[!note] Definition
>Sia $\alpha$ un numero reale positivo, si dice serie armonica generalizzata:
>
>$$
>\sum^{+\infty }_{n=1} \frac{1}{n^{\alpha}} = \begin{cases}
>\text{Converge} &se\ \ \alpha>1 \\
>\text{Diverge} &se\ \ \alpha \leq 1
>\end{cases}
>$$

- É una [[serie a termini positivi]] indipendentemente dal valore di $\alpha$.
- Quindi è non può essere una serie irregolare (indeterminata)

---
## Serie Armonica a Segni Alterni

>[!note] Definition
>Sia $\alpha$ un numero reale positivo, si dice serie armonica generalizzata:
>$$
> \sum^{+\infty }_{n=1} (-1)^{n} \frac{1}{n^{a}} = \begin{cases}
>\text{Converge assolutamente} &\text{se }\ \alpha>1 \\
\text{Diverge semplicemente} &\text{se }\ 0<\alpha<1 
\end{cases} 
>$$

Per capire meglio questi risultati leggere [[Convergenza assoluta]] [link spiegazione](https://www.youmath.it/lezioni/analisi-matematica/serie-numeriche/749-convergenza-assoluta.html)

---
## Serie Armonica Modificata

>[!note] Definition
> Sia  un numero reale positivo, si dice serie armonica modificata:
>$$
>\sum^{+\infty }_{n=2} \frac{1}{n^{\alpha}\cdot (\log n)^{\beta}} = \begin{cases}
>\text{Converge} &\text{se }\ \alpha>1 \\
>\text{Converge} &\text{se }\ \alpha=1\ \ e\ \ \beta>1 \\
>\text{Diverge positivamente} &\text{se }\ \alpha>1 \ \ e\ \ \beta \leq 1 \\
>\text{Diverge positivamente} &\text{se }\ \alpha<1
\end{cases}
>$$

---