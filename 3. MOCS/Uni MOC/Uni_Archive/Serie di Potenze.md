---
Created: 2024-04-08
Type: Uni Note
Class:
  - "[[Calcolo Integrale (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Serie]]"
  - "[[Serie di Funzioni]]"
Completed: true
---
---

>[!info] Page Index
>1. [[#Definizione]]
>2. [[#Insieme di Convergenza]]
>3. [[#Raggio di convergenza]]
>4. [[#Esempi]]

>[!info] Related
> - [[Derivata di una Serie di Potenze]]

---
## Definizione

>[!note] Definition
>Si dice serie di potenze, la serie di tipo:
>
>$$
>\textcolor{orange}{\sum^{+\infty}_{k=0} a_{ k }(x-x_{0})^{n}}= a_{0} + a_{1}(x-xo)+a_{2}(x-x_{0})^{2} +\dots+ a_{ n }(x-x_{0})^{k} \\ \\
>$$
>
>Dove:
>- $x_{0}\in\mathbb{R}$ detto cento o punto iniziale
>- $a_{k}$ una [[Successioni Reali|successone di numeri reali]]

>[!warning] oss
>- Una serie di potenze non è altro che una particolare [[Serie di Funzioni]]
>- Ogni Serie di potenze se converge converge in $x_{0}$
>- Le $x$ che fanno convergere la serie appartengono all'[[#Insieme di Convergenza]]

---
## Insieme di Convergenza 

>[!note] Definizione
>Per in insieme di convergenza ($I$) si intende un insieme di valori tali che:
>
>$$
>\forall  x \in I \to  \sum^{+\infty}_{k=0} a_{ k }(x-x_{0})^{n}\ \ \  \textcolor{orange}{\text{converge}}
>$$
>
>Ovvero insiemi di valori che se utilizzati come $x$ della serie di potenze la rendono convergente

Esistono 6 possibili Intervalli di convergenza:
1. $[\ell,\ell]\ \text{con }\ \ell \in\mathbb{R}\ \ \ \ \ \ \ \ \ \ \textcolor{orange}{\text{(un solo punto reale)}}$
2. $(-\infty,\ +\infty)\ \ \ \ \ \ \ \ \ \ \ \ \ \ \textcolor{orange}{\text{(tutto }\mathbb{R})}$ 
3. $(x_{0}−R,\ x_{0}​+R)$
4. $[x_{0}−R,\ x_{0}​+R]$
5. $(x_{0}−R,\ x_{0}​+R]$
6. $[x_{0}−R,\ x_{0}​+R)$

---
## Raggio di convergenza

>[!note] Raggio di convergenza
>In un intervallo $[x_{0}-R,\ x_{0}+R]$ $R$ è detto raggio di convergenza 

>[!warning] oss
>Due serie possono avere lo stesso raggio di convergenza ma non per questo avranno lo stesso insieme di convergenza
>
>**Infatti:** $[x_{0}-R,\ x_{0}+R] \not= (x_{0}-R,\ x_{0}+R)$

>[!tip] Calcolare raggio di convergenza
>Possiamo utilizzare [[Criterio del Rapporto e della Radice (Serie)]]
>
>$$
>\begin{align}
>&- \ \ \ \lim_{ n \to \infty }  \Big\vert \frac{a_{ n+1 }}{a_{ n }}\Big\vert = \ell\ \ \ \ \  \textcolor{orange}{\text{(rapporto)}}\\
>&- \ \ \ \lim_{ n \to \infty } \sqrt[n]{a_{ n }} = \ell\ \ \ \ \ \ \ \ \ \  \textcolor{orange}{\text{(radice)}}\\
>\end{align}
>$$
>In base al risultato del limite ($\ell$) otteniamo un $R$ diverso:
>
>$$
>R = \begin{cases}
>\infty  &\text{se } \ell = 0 \\
>0 &\text{se } \ell \not = +\infty \\ 
>\frac{1}{\ell} &\text{se } \ell \not = 0
>\end{cases}
>$$

>[!warning] oss
>- Nel caso $R=\frac{1}{\ell}$ siamo sicuri che $\forall x \in (x_{0}-R,\ x_{0}+R)$ la serie [[Criterio della convergenza assoluta (Serie)|converge assolutamente]]
>- Ma non sappiamo come la serie si comporti agli estremi dell intervallo $x_{0}-R$ e $x_{0}+R$ 
>
>Per questo dobbiamo studiare singolarmente gli esteremi e capire se convergenza assolutamente, semplicemente oppure se diverge.

---
## Esempi