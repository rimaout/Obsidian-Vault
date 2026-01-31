---
created: 2024-03-16
type: Uni Note
class:
  - "[[Calcolo Integrale (class)]]"
academic year: 2023/2024
related:
  - "[[Serie Numeriche]]"
completed: true
updated: 2026-01-31T13:32
---
---

>[!info] Index
>1. [[#Introduzione]]
>2. [[#Teorema]]
>3. [[#Teorema unito con Criterio del confronto (Gauss)]]
>4. [[#Esempi]]

---
## Introduzione
Il criterio del confronto asintotico ci permette di dire che una determinata serie $a_{n}$ ha (o no) lo stesso carattere di una serie $b_{n}$, se $a_{n}$ e $b_{n}$ sono asintoticamente equivalenti.

Questo ci permette di trovare il carattere di una serie confrontandola con serie più semplici da studiare come [[Serie Armoniche]] e [[Serie Geometriche]].

---
## Teorema

>[!note] \
>Siano $a_{ n },\ b_{n} \geq 0\ \ \forall n\in\mathbb{N}$ (successioni a [[Segno di una serie|termini positivi]]) e $b_{n}\not=0$
>
>Se:
>
>$$
>a_{ n }\sim b_{n}\ \ \ \ \ \text{Ovvero}\lim_{ n \to +\infty } \frac{a_{n}}{b_{n}} =1
>$$
>
>Allora:
>$$
>\text{Le serie } \sum^{+\infty }_{n=1} a_{n}\ e \sum^{+\infty }_{n=1}b_{n} \text{ hanno lo stesso carattere}
>$$

---
## Teorema unito con [[Criterio del confronto (Gauss - Serie)]]

Siano:
- $a_{ n },\ b_{n} \geq 0\ \ \forall n\in\mathbb{N}$ (successioni a [[Segno di una serie|termini positivi]]) 
- $b_{n}\not=0$

>[!note] $a_{ n } \sim b_{n}$
>Quando:
>$$
>\lim_{ n \to \infty } \frac{a_{ n }}{b_{n}} = \ell \in(0, +\infty )\ \  \text{(numero finito)}
>$$
>Allora:
>- $\sum a_{ n }$ ha lo stesso carattere di $\sum b_{n}$

>[!note] $a_{ n } > b_{n}$
>Quando:
>$$
>\lim_{ n \to \infty } \frac{a_{ n }}{b_{n}} = +\infty 
>$$
>Allora:
>- se $\sum b_{n}$ diverge allora $\sum a_{ n }$ diverge 

>[!note] $a_{ n }< b_{n}$
>Quando:
>$$
>\lim_{ n \to \infty } \frac{a_{ n }}{b_{n}} = 0
>$$
>Allora:
>- se $\sum b_{n}$ converge allora $\sum a_{ n }$ converge

---
## Esempi

