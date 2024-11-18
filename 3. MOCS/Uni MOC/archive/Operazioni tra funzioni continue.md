---
created: 2023-11-20
type: Uni Note
class:
  - "[[Calcolo Differenziale (class)]]"
academic year: 2023/2024
related:
  - "[[Funzioni Continue]]"
completed: true
updated: 2024-06-29T13:32
---
>[!abstract] Index
>1. [[#Proprietà]]
>2. [[#Unione intervalli funzione]]

>[!abstract] Related
>- [[Funzioni Continue]]
>- [[Funzioni]]
>- [[Calcolo Differenziale (class)]]

---
## Proprietà

Siano $\textcolor{orange}{f}$ e $\textcolor{orange}{g}$ funzioni continue:
$$
\begin{align}
&- \ \  f\pm g\ \ \ \ \ \text{è continua} \\
&- \ \ f\cdot g\ \ \ \ \ \ \ \text{è continua} \\
&- \ \ f/g\ \ \ \ \ \ \ \ \text{è continua dove g} \not= 0 \\
&- \ \ f^{g}\ \ \ \ \ \ \  \ \  \ \text{è continua}  \\
&- \ \ f(g(x))\ \ \text{è continua}
\end{align}
$$
---
## Unione intervalli funzione

Unione tra intervalli (dominio della funzione)

>[!note] Unione tra intervalli separati
>- Se $f$ è continua su $[a,b]$ e $[x,y]$ 
>- Allora $f$ è sicuramente continua su  $[a,b] \cup [x,y]$ se $b\not =x$

>[!note] Unione tra intervalli uniti
>- Se $f$ è continua su $[a,b]$ e $[b,c]$ 
>- Allora $f$ è continua in $[a,b] \cup [b,c]$ soltanto se $\underset{n \to b^{-}}{\lim}{ f(x)}$ = $\underset{n \to b^{+}}{\lim}{ f(x)}$

>[!example] Esempio
>![[Screenshot 2023-12-06 at 17.10.55.png|600]]