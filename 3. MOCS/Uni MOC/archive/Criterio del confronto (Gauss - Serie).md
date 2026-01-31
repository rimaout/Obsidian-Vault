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
>3. [[#Serie più utilizzate per il confronto]]

---
## Introduzione

Il Criteri del **confronto (Gauss)** è utilizzato per la risoluzione di **serie numeriche a termini non negativi**, confrontando la serie di una successione A con la serie di una successione B, dove **B è sempre maggiore di A**.

---
## Teorema

>[!note] \
>Supponiamo che $0\leq a_{ n }\leq b_{n}\ \ \forall n \in \mathbb{N}$ 
>
>Allora valgono le seguenti implicazioni:
>
>$$
>\begin{align}
>&1)\ \ \ \sum^{+\infty }_{n=1} b_{n}\ \textcolor{orange}{\text{Converge}}\ \ \implies \ \ \sum^{+\infty }_{n=1} a_{n}\ \textcolor{orange}{\text{Converge}} \\
>&2)\ \ \ \sum^{+\infty }_{n=1} a_{n}\ \textcolor{orange}{\text{Diverge a }+\infty }\ \ \implies \ \ \sum^{+\infty }_{n=1} b_{n}\ \textcolor{orange}{\text{Diverge a }+\infty } \\
>\end{align}
>$$

>[!warning] oss
>Le implicazioni inverse non valgono 

---
## Serie più utilizzate per il confronto

Solitamente si tende a confrontare una determinata serie con una di quest’ultime perché è facile confrontare come si comportano:
- [[Serie Geometriche]]
- [[Serie Armoniche]]

---
## Esempi