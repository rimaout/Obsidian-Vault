---
created: 2024-05-24
type: Uni Note
class:
  - "[[Calcolo Integrale (class)]]"
academic year: 2023/2024
related:
  - "[[Equazioni Differenziali]]"
completed: true
updated: 2026-01-31T13:32
---
---

>[!abstract] Index
>1. [[#Introduzione]]
>2. [[#Metodo Risolutivo]]
>3. [[#Esempi]]

>[!abstract] Related
>- [[Equazioni Differenziali]]
>- [[Calcolo Integrale (class)]]

---
## Introduzione

>[!note] Forma
>$$
>\textcolor{orange}{a}\cdot y''(x)+\textcolor{orange}{b}\cdot y'(x)+\textcolor{orange}{c}\cdot y(x)=0
>$$
>
>Dove $\textcolor{orange}{a}$, $\textcolor{orange}{b}$ e $\textcolor{orange}{c}$ $\in\mathbb{R}$

---
## Metodo Risolutivo

>[!note] 1\. Risolvere Equazione Caratteristica
>
>**Forma Eq. Caratteristica:** 
>$$
>\textcolor{orange}{a}\cdot z^{2} + \textcolor{orange}{b}\cdot z+\textcolor{orange}{c } = 0
>$$ 
>
>**Risolvere Eq.caratteristica:** 
>
>$$
>\lambda_{1},\, \lambda_{2} = \frac{-b\pm \sqrt{ b^{2}-4ac}}{2a}
>$$
>
>- Risolvere come qualsiasi altra [[Equazioni di Secondo Grado]].
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
>3. Soluzioni Complesse $(\lambda_{1,2} =\alpha\pm i\beta)$:
>$$
>\begin{align*}
>& -\ \ \textcolor{orange}{\text{Base: }}e^{\alpha x}\cos(\beta x),\, e^{\alpha x}\sin(\beta x)\\
>& -\ \ \textcolor{orange}{\text{Soluzione Generale: }} y(x)=c_{1}\cdot e^{\alpha x}\cos(\beta x)+c_{2}\cdot e^{\alpha x}\sin(\beta x)
>\end{align*}
>$$

---
## Esempi

>[!example] Esempio (soluzione reali distinte + cauchy)
>
>**Risolvere:** 
>$$
>y''-16=0
>$$
>
>**Soluzione:**
>
>![[Pasted image 20240524160813.png|700]]

>[!example] Esempio (soluzione complesse + Cauchy)
>**Risolvere:**
>
>$$
>y''(x)+4y'(t)+8y(t)=0
>$$
>
>**Soluzione:**
>![[Pasted image 20240526205817.png|650]]


