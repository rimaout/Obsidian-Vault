---
created: 2024-03-20
type: Uni Note
class:
  - "[[Calcolo Integrale (class)]]"
academic year: 2023/2024
related:
  - "[[Serie Numeriche]]"
completed: true
updated: 2024-05-27T13:29
---
---

>[!info] Index
>1. [[#Serie Esponenziale]]
>2. [[#Serie Esponenziale generalizzata]]

---
## Serie Esponenziale

La [[Serie Numeriche|serie numerica]] $\sum\limits^{+\infty}_{k=0}\frac{A^{k}}{k!}$ è detta serie esponenziale

>[!note] Studio Carattere
>Per calcolare il suo carattere possiamo utilizzare il [[Criterio del Rapporto e della Radice (Serie)|criterio del rapporto]]
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
>Funziona anche con $A<0$ infatti con $\frac{|a^{k}|}{k!}$​ possiamo utilizzare il [[Criterio di Leibniz (Serie)]]

---