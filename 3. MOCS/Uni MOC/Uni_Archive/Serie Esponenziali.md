---
Created: 2024-03-20
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
>1. [[#Serie Esponenziale]]
>2. [[#Serie Esponenziale generalizzata]]

---
## Serie Esponenziale

La serie $\sum\limits^{+\infty}_{k=0}\frac{A^{k}}{k!}$ è detta serie esponenziale

>[!note] Studio Carattere
>Per calcolare il suo carattere possiamo utilizzare il [[Criterio del Rapporto e della Radice|criterio del rapporto]]
>$$
>\lim_{ n \to +\infty } \frac{A^{k+1}}{(k+1)!} \cdot \frac{k!}{A^{k}} = \lim_{ n \to +\infty } \frac{A}{\cancel{ k! }\cdot (k+1)}\cdot \cancel{ k! } =\lim_{ n \to +\infty } \frac{1}{k+1} = 0
>$$
>Quindi la serie **converge** dato che $0<1$

---
## Serie Esponenziale generalizzata
È possibile calcolare il valore esatto di una serie esponenziale infatti:
$$
\sum^{+\infty }_{k=0} \frac{A^{k}}{k!} = e^{A}
$$

 >[!warning] oss
 >
>Funziona anche con $A<0$ infatti con $\frac{|a^{k}|}{k!}$​ possiamo utilizzare il [[Criterio di Leibniz]]

---