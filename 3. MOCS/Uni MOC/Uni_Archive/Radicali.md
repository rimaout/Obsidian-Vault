---
created: 2023-05-11
type: Uni Note
class:
  - "[[Matematica 0 (class)]]"
related:
  - "[[Condizioni di Esistenza (dominio)]]"
completed: true
updated: 2024-06-28T01:23
---

>[!abstract] Index
>1. [[#Condizioni di esistenza]]
>2. [[#Condizioni di esistenza]]
>3. [[#Teorema dei Radicali]]
>4. [[#Proprietà]]
>5. [[#Manipolazione]]

>[!abstract] Related
>- [[Matematica 0 (class)]]

---
## Introduzione

>[!note] Sintassi
>$$
>\sqrt[n]{a}
>$$
>n = ***Indice***
>a = ***Radicale***

>[!note] Caratteristiche
>Possono avvenire due casi:
>1. se `n` è **numero dispari**, si dice radice n-esima di `a` quel numero `b` che elevato ad `n` ci restituisce `a`.
>$$ se~~n~~dispari:~~ \sqrt[n]{a} \iff b^n=a,~~con~~a,b\in R $$
>
>2. se `n` è **numero pari**, si dice radice n-esima di `a` quel numero positivo `b` che, elevato ad `n`, ci restituisce un numero positivo `a` .
>$$ se~~n~~pari:~~ \sqrt[n]{a} \iff b^n=a,~~con~~a\ge 0,~~ b\ge0 $$

>[!warning] Esempio
>$$ \sqrt{-64}~~non~~esiste,~~mentre~~\sqrt[3]{-64}=-4 $$

---
## Condizioni di esistenza

$$
\sqrt[a]{x}:\ C.E.= \begin{cases}
x \in \mathbb{R}_{\geq0}\ \ \ se\ a\ pari \\
x \in \mathbb{R}\ \ \ \ \ \ se\ a\ dispari
\end{cases}
$$

---
## Teorema dei Radicali 

>[!note] Teorema
>$$
>\begin{align*}
>& - ~~se~~ a \in R_{>0} ~~ e ~~ n 1\ge\implies \exists ! ~~numeoro ~~ positivo ~~\alpha~~t.c.~~\alpha^n=a \\
>& \\
>& \textcolor{orange}{Ovvero:} ~\alpha = \sqrt[n]{a} \implies \alpha^n=a~~ dove ~~\alpha \in R_{>0} 
>\end{align*}
>$$

>[!note] Radicali come potenze con esponente fratto
>$$
>\begin{align*}
>& \sqrt[n]{a}=a^\frac{1}{n} ~~~ per~~ogni~~n\in N~~con ~~n\ge1 \\
>& \\
>& \textcolor{orange}{Nota:} ~~ \sqrt[n]{a^m}=a^{\frac{m}{n}}~~ con ~~n,m\in N \\
>\end{align*} 
>$$

>[!danger] Attenzione agli esponenti negativi
>$$
>a^{-\frac{m}{n}} \coloneqq \frac{1}{\sqrt[n]{a^m}}
<$$

---
## Proprietà

>[!note] Proprietà
>$$
>\begin{align*}
>& 1.~~~~ \sqrt[n]{a} * \sqrt[n]{b}=\sqrt[n]{ab} \textcolor{orange}{\dashrightarrow Prodotto ~~di~~ radicali~~con~~stesso~~indice} \\
>& \\
>& 2.~~~~ \frac{\sqrt[n]{a}}{\sqrt[n]{b}}=\sqrt[n]{\frac{a}{b}}~~~ dove~~b\not =0 \textcolor{orange}{ \dashrightarrow Differenza ~~tra~~ due~~radicali~~stesso~~indice}\\
>& \\
>& 3.~~~~ \sqrt[n*s]{a^{m\cdotp s}}=\sqrt[n]{a^m}\textcolor{orange}{\dashrightarrow Proprieta' ~~invariantiva}\\
>& \\
>& 4.~~~~ (\sqrt[n]{a})^m=\sqrt[n]{a^m}~~\forall a\ge 0, ~con~n,m \in N \textcolor{orange}{\dashrightarrow Potenza~ di~ un~ radicale}
>& \\ \\
>& 5.~~~~\sqrt[m]{\sqrt[n]{a}}= \sqrt[m\cdotp n]{a}~~con~~m,n\in N \textcolor{orange}{\dashrightarrow Radice~~di~~radice}\\
>\end{align*} 
>$$
>
>>**OSS:**
>>$$
>>\begin{align*}
>>& 1. ~~~\sqrt[n]{a+b} \not = \sqrt[n]{a}+\sqrt[n]{b} \\
>>&\\
>>& 2.~~~\sqrt[n]{-a} = -\sqrt[n]{a}\\
>>\end{align*}
>>$$

---
## Manipolazione

>[!note] Trasporto di un fattore dentro il segno di radice
>$$a\sqrt[n]{b} = \sqrt[n]{a^n \cdot b} ~~~ con~~a,b\ge0,~~n \in N$$

>[!note] Riduzione di due radicali allo stresso indice
>$$\sqrt[n]{a}, ~~ \sqrt[m]{b}$$
>
>1. Calcolare [[minimo comune multiplo]] tra *n* ed *m*
>2. Utilizziamo l'[[mcd]] come nuovo esponente delle radici
>3. Dividiamo il nuovo indice per i rispettivi indici delle radici
>4. Eleviamo i radicandi al risultato precedente (3)
>
>>[!warning] Esempi
>>$$
>>\begin{align*}
>>& 0.~~~~  \sqrt[3]{8}, ~~ \sqrt[4]{16}\\
>>& \\
>>& 1.~~~~ m.c.d.(3,4) = 12\\
>>& \\
>>& 2.~~~~ \sqrt[12]{8^x}, ~~ \sqrt[12]{16^y}\\
>>& \\
>>& 3.~~~~ x = 12/3, ~~y=12/4\
>>& \\
>>& \\
>>& 4.~~~~ \sqrt[12]{8^4}, ~~ \sqrt[12]{16^3}\\
>>\end{align*}
>>$$
