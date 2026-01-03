---
created: 2023-10-02
type: Uni Note
class:
  - "[[Calcolo Differenziale (class)]]"
academic year: 2023/2024
related:
  - "[[Teoria degli insiemi]]"
  - "[[Estremo Superiore e Inferiore, Massimo, Minimo, Maggiorante e Minorante di un insieme]]"
completed: true
updated: 2024-06-28T14:08
---

>[!abstract] Index
>1. [[#Definizioni]]
>2. [[#Operazioni]]
>3. [[#Maggiorante e Minorante]]
>4. [[#Estremo superiore e Inferiore]]
>5. [[#Massimo e Minimo]]

>[!abstract] Related
>- [[Calcolo Differenziale (class)]]

---
## Definizioni

>[!note] Intervalli chiusi
>$$
>\begin{align}
>& [a,b]=\{x \in \mathbb{R}: a \leq x \leq b \} \\
>& [a,b)=\{x \in \mathbb{R}: a \leq x < b \} \\
>& (a,b]=\{x \in \mathbb{R}: a < x \leq b \} \\
>& (a,b)=\{x \in \mathbb{R}: a < x < b \} \\
>\end{align}
>$$

>[!note] Intervalli aperti
>$$
>\begin{align}
>& (- \infty,b)= \{x \in \mathbb{R}: x < b \} \\
>& (- \infty,b]= \{x \in \mathbb{R}: x \leq b \}  \\
>& (a,+\infty)=  \{x \in \mathbb{R}: x > a \} \\
>& [a, +\infty)= \{x \in \mathbb{R}: x \geq a \} \\ \\
>&\text{oss: }\ (+ \infty,- \infty):= \mathbb{R}  \\
>\end{align}
>$$

---
## Operazioni

>[!note] Unione tra intervalli
> L'unione tra due intervalli non da necessariamente come risultato un intervallo
>$$
>\begin{align}
>&(0,1)\cup[1,2] = (0,2) \ \ \ \ \textcolor{orange}{\text{è intervallo}} \\\\
>& (0,1)\cup[2,3] \ \ \ \ \textcolor{orange}{\text{non è intervallo}} \\ 
>& (0,1) \cup (1,2)\ \ \  \textcolor{orange}{\text{non è intervallo}} \\
>\end{align}
>$$
>
>>[!warning] oss
>>$$
>>\{0\}\cup\{1\} \ \ \ \ \textcolor{orange}{\text{non è un intervallo} }
>>$$

>[!note] Intersezione tra intervalli
>Intersezione tra due intervalli è un intervallo se l'intersezione non è vuota e diversa da un solo punto.

---
## Maggiorante e Minorante

>[!note] Maggiorante
>Si dice maggiorante di `A` un qualsiasi valore reale (`y`) che maggiora tutti gli elementi (`x`) dell'insieme (`A`)
>
>$$
>\begin{align}
>& A\subseteq \mathbb{R} \\
>& y\in \mathbb{R}\ \text{maggiorante }A \iff \forall x \in A: y \geq x \\
>\end{align}  
>$$

>[!note] Minorante
Si dice minorante di `A` un qualsiasi valore reale (`y`) che minora tutti gli elementi (`x`) dell'insieme (`A`)
>$$
>\begin{align}
>& A\subseteq \mathbb{R} \\
>& y\in \mathbb{R}\ \text{minorante }A \iff \forall x \in A: y \leq x \\
>\end{align}  
>$$
>
>>**oss:** ﻿﻿per far sì che un valore reale sia un minorante o un maggiorante di un insieme, può appartenervi o non appartenervi

---
## Estremo superiore e Inferiore

>[!note] Estremo superiore
>$$sup(A)=y$$
>`y` si dice **Estremo Superiore** di `A` se `y` è il **piccolo maggiorante** di A.

>[!note] Estremo inferiore
>$$inf(A)=y$$
>`y` si dice **Estremo Inferiore** di `A` se `y` è il **grande minorante** di A.

>[!warning] oss
>1. Estremo superiore ed inferiore esistono sempre se l'insieme non è vuoto
>2. Estremo superiore ed inferiore posso e non possono far parte dell' insieme 

>[!note] Proprietà
>$$\begin{align}
>& 1. \ \ \ \ se\ \ A\not=\emptyset \implies\ inf(A)\leq sup(A) \\
>& 2. \ \ \ \ se\ A\subseteq B \implies inf(B)\leq inf(A)\leq sup(A)\leq sup(B) \\
>& 3. \ \ \ \ se\ \forall a \in A\ \exists b \in B:\ a\leq b \implies\sup(A)\leq sup(B) \\
>& 4. \ \ \ \ se\ \forall a \in A\ \exists b \in B:\ a\geq b \implies\inf(B)\leq inf(A) \\
>\end{align}
>$$

---
## Massimo e Minimo

>[!note] Massimo
>Se l'estremo superiore di un insieme appartiene all'insieme stesso, allora prende il nome di massimo dell'insieme.
>$$
>\begin{align}
>& A\subseteq \mathbb{R} \\
>& max(A)=y\iff y=sup(A)\land y\in A\\
>\end{align}
>$$

>[!note] Minimo
>Se l'estremo inferiore di un insieme appartiene all'insieme stesso, allora prende il nome di minimo dell'insieme.
>
>$$
>\begin{align}
>& A\subseteq \mathbb{R} \\
>& min(A)=y\iff y=inf(A)\land y\in A\\
>\end{align}
>$$
