---
Created: 2024-03-01
Type: Uni Note
Class:
  - "[[Calcolo Integrale (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Serie Numeriche]]"
Completed: true
---
---

>[!info] Indice
>1. [[#Serie geometriche]]
>2. [[#Somme parziale geometrica]]
>3. [[#^bf34ea|Limite di somme parziali geometriche]]
---

---
## Serie geometriche 

>[!note] Definizione
>La serie:
>$$
>S_{ n } =\sum^{\infty}_{n=0}q^{n}
>$$ 
>dove $q \in \mathbb{R}$ è detta **serie geometrica di ragione q**

---
## Somme parziale geometrica

>[!note] Definizione
>$$
>S_{ n } = \sum^{n}_{=0}q^{k} = 1 + q + q^{2} + \dots + q^{n} = \begin{cases}
>\frac{1-q^{n+1}}{1-q} &\text{se }\ q \not= 1 \\
>n+1 &\text{se }\ q = 1
>\end{cases}
>$$

>[!danger] Limite di somma parziale geometrica
>
>$$
>\lim_{ n \to \infty } S_{ n } = \begin{cases}
> +\infty  &\text{se}\ \ q\geq 1 \\
>\frac{1}{1-q} &\text{se}\ \ -1<q<1\ \ \  (q\not= 0)\\
>\text{non esiste} & \text{se }\ \ q\leq 1
>\end{cases}
>$$
>Quindi:
>$$\sum^{\infty }_{n=0}q^{n}\ \text{ è} \begin{cases}
>\text{Divergente} &\text{se}\ \ q\geq 1 \\
>\text{Convergente (ad } \frac{1}{1-q} \text{)} &\text{se}\ \ -1<q<1\ \ \ (q\not= 0) \\
>\text{Indeterminata} & \text{se }\ \ q\leq 1
>\end{cases}$$

^bf34ea

>[!example] Esempio:
>![[Pasted image 20240301161032.png|600]]
