---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2024-10-30T12:26
updated: 2024-10-30T12:50
---
>[!abstract] Index
>1. 

>[!abstract] Related
>- 

>[!danger] TLDR

---
cosa con variabili aleatorie (funzioni) composte

>[!example] Esempio
>Lanciamo 10 volte una monete e definiamo una variabile aleatoria $X$ tale che $X := \#\text{Numero di Teste (T) uscite}$
>
>Vinco 2 euro per ogni testa e perdo 1 euro per ogni croce, definiamo una variabile aleatoria $Y$ tale che $Y := \# \text{Guadagno finale}$
> 
>Posso esprimere $Y$ come $f(X)$:
>- $Y = 2 \cdot X - 1 \cdot(10-x) = 3x - 10$ 
>  $Y = f(x)$ dove $f: \mathbb{R}\to \mathbb{R}$
>  
>Hi (S,P)
>Ho $X: S \to S$ v.a.
>Ho $f:\mathbb{R}\to \mathbb{R}$
>
>Se $X$ è una fariabile discreta, allora $f \circ g = f(X)$  è variabile discreta
>
>Mi interessa calcolare $E[f(x)]$
>
>**1° Modo:** Determiniamo i possibili valori di $f(x)$ che chiamiamo $\{  y_{j}\mathbf{j} \in J \}$ e calcolo:
>
>$$
>P(f(x) = y') \ \ \forall  i \in J 
>$$
>
>Perche:
>$$
>E[f(x)] = \sum_{j} y_{j} \cdot  p(f(x) = y_{j})
>$$
>
>**Secondo modo:**
>
>vljesjlskvbdkbfe


>[!danger] Teorem
>sia $X$ v.a. disxreta che assume i calori $\{ x_{i} \}_{i \in I}$ 
>sia $f:\mathbb{R}\to \mathbb{R}$
>
>Allora:
>$$
>\begin{align*}
>E[f(x)] & = \sum_{i \in I} f(x_{i}) P(X=x_{i}) \\
>& = \sum_{i=I} f(x_{i}) P(x_{i})P_{X}(x_{i})
>\end{align*}
>$$

>[!example] Example:
>Sia X v.a. che assume valori -1,0,3 con prob. 0.2, 0.5, 0.3 rispettivamente 
>
>Calcolare $E((x-1)^{2})$
>
>avendo 3 valori nonc'è molto vantaggio di usare un metodo aziche l'altro
>
>**Metodo 1:** $Y := (x-1)^{2}$ assume valori 4,1
>
>| X | Y |
>| --- | --- |
>| -1 | 4
>| 0 | 1 |
>| 3 | 4 |
>
>- P(y=4) = P(x-2) + P(X = 3) = 0.2 + 0.3 = 0.5
>  P()vncsjzdvnkjn sklj
>
>$E[Y] = 4 \cdot 0.5 + 1 \cdot 0.5 = 2.5$
>
>**Metodo 2:**
>
>ljlkjenslkjfnelj
