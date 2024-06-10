---
created: 2023-05-11
type: Uni Note
class:
  - "[[Matematica 0 (class)]]"
related: 
completed: true
updated: 2024-06-08T11:18
---
---
## Indice
1. [[#Sintassi]]
2. [[#Teorema]]
3. [[#Condizioni di esistenza]]
4. [[#Proprietà]]

---
## Sintassi 

$$ \log_a b$$
- *a* = Base
- *b* = Argomento 

*Si legge:* logaritmo in base a di b

---
## Teorema 

$$
\begin{align*}
& se ~~ a,b>0 ~~ e ~~ a \not = 1 \implies \exists ~ \alpha~~t.c.~~ a^\alpha = b \\
& \\
& \textcolor{orange}{Ovvero:} ~\alpha = \log_ab \implies a^\alpha = b
\end{align*}
$$

---
## Condizioni di esistenza

$$
\log_{f(x)}[g(x)]: C.E
\begin{cases}
   f(x)>0 \\
   f(x)\neq 1 \\
   g(x)>0
\end{cases} 
$$

---
## Proprietà 
$$
\begin{align*}
& 1.~~~~ \log_ab \cdot c =  \log_ab~~ + ~~\log_ac \textcolor{orange}{\dashrightarrow Prodotto ~~tra~~ logaritmi} \\
& \\
& 2.~~~~ \log_a\frac{b}{c} =  \log_ab~~ - ~~\log_ac  \textcolor{orange}{\dashrightarrow Differenza ~~tra~~ logaritmi}\\
& \\
& 3.~~~~ \log_ab^n =  n \cdot \log_ab \textcolor{orange}{\dashrightarrow Potenza~~di~~ un~~logaritmo}\\
& \\
& 4.~~~~ \log_ab= \frac{\log_cb}{\log_ca} \textcolor{orange}{\dashrightarrow Cambio ~~ base}\\
& \\
& 5.~~~~ x^{\log_b y} = y^{\log_{b} x}
\end{align*}
$$

**oss:** 
$$
\begin{align*}
& - se~~a>0 ~~ m>n \implies \log_am > \log_an \textcolor{orange}{\dashrightarrow Crescente} \\
& \\
& - se~~a<0 ~~ m>n \implies \log_am < \log_an \textcolor{orange}{\dashrightarrow Decrescente}  \\
\end{align*}
$$

>[!warning] Esempio Cambio Base
> $$
> n\log_2 n=(2^{\log_2 3})^{\log_2 n}= 2^{(\log_2 n)*(\log_2 3)}=(2^{\log_2 n})^{\log_2 3} =n^{\log_2 3}
> $$

---
