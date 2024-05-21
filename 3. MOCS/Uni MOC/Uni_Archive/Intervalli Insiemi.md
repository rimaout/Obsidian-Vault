---
Created: 2023-10-02
Type: Uni Note
Class:
  - "[[Calcolo Differenziale (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Teoria degli insiemi]]"
  - "[[Estremo Superiore e Inferiore, Massimo, Minimo, Maggiorante e Minorante di un insieme]]"
Completed: true
---
---
## Indice
1. [[#Definizioni]]
2. [[#Operazioni]]
3. [[#Maggiorante e Minorante]]
4. [[#Estremo superiore e Inferiore]]
5. [[#Massimo e Minimo]]
6. [[#Esempi]]

---
## Definizioni

**Intervalli chiusi:**
$$
\text{È un intervallo di } \mathbb{R}:
\begin{align}
& [a,b]=\{x \in \mathbb{R}: a \leq x \leq b \} \\
& [a,b)=\{x \in \mathbb{R}: a \leq x < b \} \\
& (a,b]=\{x \in \mathbb{R}: a < x \leq b \} \\
& (a,b)=\{x \in \mathbb{R}: a < x < b \} \\
\end{align}
$$

**Intervalli aperti:**
$$
\begin{align}
& (- \infty,b)= \{x \in \mathbb{R}: x < b \} \\
& (- \infty,b]= \{x \in \mathbb{R}: x \leq b \}  \\
& (a,+\infty)=  \{x \in \mathbb{R}: x > a \} \\
& [a, +\infty)= \{x \in \mathbb{R}: x \geq a \} \\ \\
& (+ \infty,- \infty):= \mathbb{R}  \\
\end{align}
$$

---
## Operazioni
**Unione tra intervalli:**
- L'unione tra due intervalli non da necessariamente come risultato un intervallo
$$
\begin{align}
&(0,1)\cup[1,2] = (0,2) \ \ \ \ \textcolor{orange}{\text{è intervallo}} \\\\
& (0,1)\cup[2,3] \ \ \ \ \textcolor{red}{\text{non è intervallo}} \\ 
& (0,1) \cup (1,2)\ \ \  \textcolor{red}{\text{non è intervallo}} \\
\end{align}
$$

*oss:*

$$
\{0\}\cup\{1\} \ \ \ \ \textcolor{red}{\text{non è un intervallo} }
$$

**Intersezione tra intervalli:**
Intersezione tra due intervalli è un intervallo se l'intersezione non è vuota e diversa da un solo punto

---
## Maggiorante e Minorante

**Maggiorante** di A:
-  è un qualsiasi valore reale (*y*)che maggiora tutti gli elementi (*x*) dell'insieme (*A*)

$$
\begin{align}
& A\subseteq \mathbb{R} \\
& y\in \mathbb{R}\ \text{maggiorante }A \iff \forall x \in A: y \geq x \\
\end{align}  
$$

**Minorante** di A:
- è un qualsiasi valore reale (*y*) che minora tutti gli elementi (*X*) dell'insieme. (*A*)
$$
\begin{align}
& A\subseteq \mathbb{R} \\

& y\in \mathbb{R}\ \text{minorante }A \iff \forall x \in A: y \leq x \\
\end{align}  
$$

*oss:* ﻿﻿per far sì che un valore reale sia un minorante o un maggiorante di un insieme, può appartenervi o non appartenervi

---
## Estremo superiore e Inferiore
di un insieme insieme reale
**Estremo superiore:**
$$sup(A)=y$$
- Se y è il piccolo maggiorante di A

**Estremo inferiore:**
$$inf(A)=y$$
- Se y è il grande minorante di A

*oss:* 
1. Estremo superiore ed inferiore esistono sempre se l'insieme non è vuoto
2. Estremo superiore ed inferiore posso e non possono far parte dell' insieme 

**Proprietà:**
$$\begin{align}
& 1. \ \ \ \ se\ \ A\not=\emptyset \implies\ inf(A)\leq sup(A) \\
& 2. \ \ \ \ se\ A\subseteq B \implies inf(B)\leq inf(A)\leq sup(A)\leq sup(B) \\
& 3. \ \ \ \ se\ \forall a \in A\ \exists b \in B:\ a\leq b \implies\sup(A)\leq sup(B) \\
& 4. \ \ \ \ se\ \forall a \in A\ \exists b \in B:\ a\geq b \implies\inf(B)\leq inf(A) \\
\end{align}$$

---
## Massimo e Minimo
**Massimo:**
Se l'estremo superiore di un insieme appartiene all'insieme stesso, allora prende il nome di massimo dell'insieme.
$$\begin{align}
& A\subseteq \mathbb{R} \\
& max(A)=y\iff y=sup(A)\land y\in A\\

\end{align}  $$
**Minimo:**
Se l'estremo inferiore di un insieme appartiene all'insieme stesso, allora prende il nome di minimo dell'insieme.
$$\begin{align}
& A\subseteq \mathbb{R} \\
& min(A)=y\iff y=inf(A)\land y\in A\\

\end{align}  $$
