---
Created: 2024-03-16
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
>1. [[#Introduzione]]
>2. [[#Teorema]]
>3. [[#Esempi]]

---
## Introduzione 

I Criteri del **Rapporto** e della **Radice** sono utilizzati per la risoluzione di **serie numeriche a termini non negativi**

---
## Teorema 

>[!note] \
Sia $a_{ n }>0\ \ \forall n \in \mathbb{N}$  (serie a termini positivi)
>
>Supponiamo che:
>
>$$
>\begin{align}
>&\lim_{ n \to +\infty } \frac{a_{ n+1 }}{a_{ n }} = \ell\ \ \ \ \textcolor{orange}{\text{(Rapporto)}} \\
>&\lim_{ n \to +\infty } \sqrt[n]{a_{ n }} = \ell\ \ \ \ \ \ \textcolor{orange}{\text{(Radice)}}
>\end{align}
>$$
>Allora:
>
>$$
>\sum^{+\infty }_{n=1}a_{ n } \begin{cases}
>\text{Converge} &\text{Se }\ 0\leq \ell <1 \\
>\text{Diverge }(+\infty ) &\text{Se }\ \ell>1 \\
>\text{Indeterminato (usare altro metodo)} &\text{Se }\ \ell=1
\end{cases}
>$$

>[!warning] oss
>- Questi due metodi sono equivalenti (utilizzare quello più semplice per ogni determinata successione)
>- Essendo $a_{ n >0}$ $\implies$ $\ell \in[0,+\infty)$ oppure $\ell=+\infty$
>- Se $a_{ n }= \frac{1}{n^{\alpha}}$ i due metodi falliscono ($\ell=1$)

---
## Esempi

![[Pasted image 20240316112523.png|800]]

![[Pasted image 20240316112910.png|800]]

![[Pasted image 20240316113012.png|800]]

---