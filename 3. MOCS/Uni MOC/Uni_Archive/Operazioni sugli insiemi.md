---
created: 2023-09-28
type: Uni Note
class:
  - "[[Metodi matematici per l'informatica (class)]]"
  - "[[Matematica Discreta (class)]]"
academic year: 2022/2023
related:
  - "[[Teoria degli insiemi]]"
completed: true
updated: 2024-05-27T13:29
---
---
## Indice
1. [[#Appartenenza]]
2. [[#Inclusione]]
3. [[#Unione]]
4. [[#Intersezione]]
5. [[#Differenza]]
6. [[#Complemento]]
7. [[#Prodotto cartesiano]]
8. [[#Insiemi delle parti]]

---
## Appartenenza
$$x \in A$$
- x è elemento che appartiene ad A
- Può essere vero o falso 

---
## Inclusione
**Sottoinsieme proprio o inclusione stretta:** 
$$A \subset B$$

Sottoinsieme A è contenuto nell'insieme B, ma esiste almeno un elemento di B che non è contenuto in A
![[IMG_2D5F229F8E7B-1.jpeg]]
**Sottoinsieme improprio:**
$$ A \subseteq B$$
Nell'inclusione normale (A⊆B) invece i due insiemi possono anche essere uguali (A=B)
**oss:** $$A=B \iff (A\subseteq B) \land(B\subseteq A))$$

---
## Unione
$$A \ \cup \ B = \{ x: \ x\in A \text{ oppure }x\in B \}$$
Un elemento o appartiene ad A o appartiene a B![[IMG_DA4027BDD4EC-1.jpeg]]

**Proprietà:**
$$\begin{align}
&1. \ \ \ \ A\cup \emptyset =A \\
&2. \ \ \ \ A\cup B=B\cup A\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \textcolor{orange}{\text{ prop. commutativa}} \\
&3. \ \ \ \ (A\cup B)\cup C=A\cup(B\cup C)\ \ \ \textcolor{orange}{\text{ prop. associativa}}\\
&4. \ \ \ \ A\cup A = A \\
&5.\ \ \ \ B \subseteq A \implies A\cup B = A \\

\end{align}$$
---
## Intersezione
Un elemento appartiene sia ad A che a B
$$A \ \cap \ B = \{ x: \ x\in A \text{ e }x\in B \}$$
![[IMG_7C96C924E8EE-1.jpeg]]

**Proprietà:**
$$ \begin{align}
&1. \ \ \ \ A\cap \emptyset = \emptyset\\
&2. \ \ \ \ A\cap B=B\cap A\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \textcolor{orange}{\text{ prop. commutativa}} \\
&3. \ \ \ \ (A\cap B)\cap C=A\cap(B\cap C)\ \ \ \textcolor{orange}{\text{ prop. associativa}}\\
&4. \ \ \ \ A\cap A = A \\
&5.\ \ \ \ B \subseteq A \implies A\cap B = B \\

\end{align}$$

---
## Differenza

$$A \text{ \\ }B == \{ x: \ x\in A \text{ e }x\not\in B \}  $$
Un elemento appartiene ad A ma non a B
![[IMG_1FD001944879-1.jpeg]]

**Proprietà:**
$$A-B \not= B-A$$
$$se\ A = B \implies A-B=\{ \emptyset \}$$
---
## Complemento
$$A^C := \{ x \in E: x\not\in A \}$$
Dato un insieme A sotto insieme di E (insieme universo E), si definisce insieme complementare di A,  *l'insieme degli elementi che non appartengono ad a ma che sono contenuti in E*

![[IMG_458D0A863DC2-1.jpeg]]

**oss:**
$$
\begin{align} \\
& \text{se } A\subseteq E \implies A^C =E/A

\end{align}
$$
---
## Prodotto cartesiano 
$$ A\times B=\{(a,b)|\ a\in A,\ b \in B \} $$
Prodotto cartesiano tra gli insiemi A e B è l'insieme che ha per elementi tutte le possibili coppie ordinate (a, b) 

Dove:
- a sono tutti gli elementi dell'insieme A 
- b sono tutti gli elementi dell'insieme B

**Esempio:**
![[IMG_014F169AAD4F-1.jpeg]]

---
## Insiemi delle parti
L'insieme delle parti di A è l'insieme che ha come elementi tutti i possibili sottoinsiemi dell'insieme A.
$$ P_{A} = \{B|B \subset A\} $$


**oss:**$$\begin{align}
& A \in P(A) \\
& \emptyset \in  P(A)\\
\end{align}$$
$$\begin{align}
& - \ \ \text{Cardinalità P(A)}= 2^n \\ 
& -\ \ \text{Dove n è la cardinalità di A}
\end{align}$$

**Esempio:**![[IMG_2094.jpg]]

---