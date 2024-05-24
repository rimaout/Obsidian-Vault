---
Created: 2024-05-24
Type: Uni Note
Class:
  - "[[Calcolo Integrale (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Equazioni Differenziali]]"
Completed: false
---
---

>[!abstract] Index
>1. 

>[!abstract] Related
>- [[Equazioni Differenziali]]
>- [[Calcolo Integrale (class)]]

---
## Introduzione

>[!note] Forma
>$$
>\textcolor{orange}{a}y''\cdot (x)+\textcolor{orange}{b}y'\cdot (x)+\textcolor{orange}{c}\cdot y(x)=0
>$$
>
>Dove $\textcolor{orange}{a}$, $\textcolor{orange}{b}$ e $\textcolor{orange}{c}$ $\in\mathbb{R}$

---
## Metodo Risolutivo

>[!note] 1\. Risolvere Equazione Caratteristica
>
>**Forma Eq.Catatteristica:** 
>$$
>\textcolor{orange}{a}\cdot z^{2} + \textcolor{orange}{b}\cdot z+\textcolor{orange}{c } = 0
>$$ 
>
>**Risolvere Eq.caratteristica:** Come qualsiasi altra [[Equazioni di Secondo Grado]].
>$$
>\lambda_{1},\, \lambda_{2} = \frac{-b\pm \sqrt{ b^{2}-4ac}}{2a}
>$$
>
>**Calcolare Soluzione Generale:**
>Esistono 3 possibili soluzione diverse in base al risultato dell'equazione caratteristica:
>1. Soluzioni Reali Distinte $(\lambda_{1}\not =\lambda_{2})$:
>$$
>\begin{align*}
>& -\ \ \textcolor{orange}{\text{Base: }}e^{\lambda_{1}x},\, e^{\lambda_{2}x}\\
>& -\ \ \textcolor{orange}{\text{Soluzione Generale: }} y(x)=c_{1}\cdot e^{\lambda_{1}x}+c_{2}\cdot e^{\lambda_{2}x}
>\end{align*}
>$$
>
>2. Soluzioni Reali Coincidenti $(\lambda_{1} =\lambda_{2})$:
>$$
>\begin{align*}
>& -\ \ \textcolor{orange}{\text{Base: }}e^{\lambda x},\, xe^{\lambda x}\\
>& -\ \ \textcolor{orange}{\text{Soluzione Generale: }} y(x)=c_{1}\cdot e^{\lambda x}+c_{2}\cdot xe^{\lambda x}
>\end{align*}
>$$
>
>3. Soluzioni Reali Coincidenti $(\lambda_{1,2} =\alpha\pm i\beta)$:
>$$
>\begin{align*}
>& -\ \ \textcolor{orange}{\text{Base: }}e^{\alpha x}\cos(\beta x),\, e^{\alpha x}\sin(\beta x)\\
>& -\ \ \textcolor{orange}{\text{Soluzione Generale: }} y(x)=c_{1}\cdot e^{\alpha x}\cos(\beta x)+c_{2}\cdot e^{\alpha x}\sin(\beta x)
>\end{align*}
>$$

---
## Esempi

>[!example] Esempio
>
>**Risolvere:** 
>$$
>y''-16=0
>$$
>
>**Soluzione:**
>
>![[Pasted image 20240524160813.png|700]]

