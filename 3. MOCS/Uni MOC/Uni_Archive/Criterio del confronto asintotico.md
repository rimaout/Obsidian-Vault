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
## Teorema unito con [[Criterio del confronto (Gauss)]]

>[!note] \
>Siano $a_{ n },\ b_{n} \geq 0\ \ \forall n\in\mathbb{N}$ (successioni a [[Segno di una serie|termini positivi]]) e $b_{n}\not=0$
>
>Dove:
>$$
>\lim_{ n \to +\infty }  \frac{a_{ n }}{b_{n}} = \ell
>$$
>
>Se:
>- $\ell \in(0,+\infty) \implies \sum\limits^{+\infty }_{n=1} a_{n} = \sum\limits^{+\infty }_{n=1}b_{n}$
>- $\ell =0 \text{ e}\sum\limits^{+\infty }_{n=1}b_{n} \text{ Converge}\implies \sum\limits^{+\infty }_{n=1} a_{n} \text{ Converge}\ \ \ \ \text{oss: }b_{n}<a_{ n }$
>- $\ell =+\infty\ \text{ e}\sum\limits^{+\infty }_{n=1}b_{n} \text{ Diverge}\implies \sum\limits^{+\infty }_{n=1} a_{n} \text{ Diverge}\ \ \ \ \text{oss: }b_{n}>a_{ n }$

---
## Esempi

