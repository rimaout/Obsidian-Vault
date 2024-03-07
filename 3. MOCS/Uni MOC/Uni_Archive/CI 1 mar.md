---
Created: 2024-03-01
Type: Uni Note
Class:
  - "[[Calcolo Integrale (class)]]"
Academic Year: 2023/2024
Related: 
Completed: false
---
---
## Index
1. [[#Serie]]
2. [[#Serie geometriche]]

---

## Serie


se $a_{n}$ è definitivamente (pen n abbastanza grande) uguale a zero allora $\sum^{+\infty}_{n=0}a_{n}$ converge


---

>[!danger] Teorema
>- Sia $\exists r \in\mathbb{R}>0$
>- Se $a_{n}\geq r$
>- Allora $\sum^{+\infty}_{n=1}=+\infty$

>[!example] Example:
>$$
>a_{n}=(-1)^{n} \implies \sum^{+\infty }_{n=1} (-1)^{n}\ \text{ è indeterminata}
>$$

---
>[!danger] Teorema
>- Sia $\{a_{n}\}$ una successione 
>- Se $\sum^{+\infty}_{n=1}a_{n}$ converge 
>- Allora $\{ a_{n} \}$ è un infinitesimo (ovvero che $\lim_{ n \to \infty }a_{ n } \to 0$)

>[!warning] Dimostrazione
>- $S_{n} = a_{1} + a_{2}+ \dots + a_{n-1} + a_{n}$
>- $S_{n-1}= a_{1} + a_{2} + \dots + a_{n-1}$
>- $a_{n} = S_{n}-S_{n-1}$
>
>Quindi:
>- $\lim_{ n \to +\infty }a_{n}=\lim_{ n \to +\infty }S_{n}-S_{n-1} =\lim_{ n \to +\infty} S_{n}+ \lim_{ n \to +\infty} S_{n-1}=S-S=0$

**Domanda:** se $a_{ n }$ è infinitesima $\implies$ $\sum^{+\infty}_{n=1}a_{ n }\ \ converge?$ **NO** 

**Contro esempio:** 
![[Pasted image 20240301101716.png|600]]

---
## Serie geometriche
