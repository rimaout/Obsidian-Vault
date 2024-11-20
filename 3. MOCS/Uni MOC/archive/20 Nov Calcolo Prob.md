---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2024-11-20T14:18
updated: 2024-11-20T14:59
---
>[!warning] oss
>Data una funzione la cardinalità del condominio è sempre minore uguale della cardinalità del dominio.

data $f: \mathbb{R}^{2} \to R$ ho che $f(X,Y):S \to \mathbb{R}$

$f(X,Y)$ è v.a. discreta quindi possiamo calcolare $E\big[f(X,Y)\big]$ con la definizione di:
$$
E\big[ f(X,Y) \big] = \sum_{z}z\cdot P(f(X,Y) = z)
$$

Dove $z$ sono i valori assunti dalla variabile aleatoria $f(X,Y)$

>[!warning] Prop
>Siano $X$ e $Y$ v.a. discrete e sia $f:\mathbb{R}^{2} \to R$, allora:
>$$
>E[f(X;Y)] = \sum_{i\in I} \sum_{j\in J} f(x_{i}, y_{j}) P_{X,Y} (x_{i}, y_{j})
>$$
>
>Dove 
>- $\{ X_{i} \}_{i \in I}$ è l'insieme dei possibili valori di $X$
>- $\{ Y_{j} \}_{j \in J}$ è l'insieme dei possibili valori di $Y$
>  
>  Con tre variabili
>  
>$$
>E\big[f(X,Y,Z)\big] = \sum_{i} \sum_{j} \sum_{k} Plkcasln
>$$

>[!example] Example:
>Vedi ipad 1° esempio

>[!warning] Prop
>$$
>E[X+Y] = E[X] + E[Y]
>$$
>
>>[!warning] Dim
>>- $f: \mathbb{R}^{2} \to \mathbb{R}$
>>- $f(a,b) = a+b$
>>- $f(X,Y) = X + Y$

$$
\begin{align*}
E[X+Y] &= E[f(X;Y)] \\
& \ \ |\\
&= \sum_{i} \sum_{j} f(x_{i},y_{j})P_{X,Y}(x_{i},y_{j})\\
& \ \ | \\
&= \sum_{i} \sum_{j} x_{i}P_{X,Y}(x_{i},y_{j}) + \sum_{i} \sum_{j} y_{j} P_{X,Y}(x_{i},y_{j})\\
& \ \ | \\
& =E[X] + E[Y]
\end{align*}
$$

>[!warning] Prop
>
>$$
>E[X_{1} + \dots+ x_{n}] = E[X_{1}] + \dots + E[X_{n}]
>$$
>
>più in generale dai $a_{1}, a_{2}, \dots , a_{n} \in \mathbb{R}$

>[!warning] Prop
>
>$$
>E[a_{1}X_{1} + \dots+ a_{n}x_{n}] = a_{1}E[X_{1}] + \dots + a_{n}E[X_{n}]
>$$
>
>più in generale dai $a_{1}, a_{2}, \dots , a_{n} \in \mathbb{R}$

>[!example] Lancio un dado 1000 volte calcolano senza usare formulari, $E[X]$ dati $X = \#\text{volte in cuiesce 5}$
>
>$X = \text{Bin}\left( n=1000,p=\frac{1}{6}  \right)$
>
>Sappiamo che: $E[X] = \sum_{k=0}^{1000}k P(X=k) = \sum^{1000}_{k=0} k \binom{1000}{k}p^{k}(1-p)^{1000} = \sum^{1000}_{k=0} \binom{1000}{k} \left( \frac{1}{6} \right)^{k}\left( \frac{5}{6} \right)^{1000-k}$
>
>Ma questo metodo è molto lungo e faticosa, possiamo usare questo altro metodo più breve:
>
>introduciamo 1000 variabile aleatorie $X_{1}, \dots, X_{i}$ con $i$ che va da 1 a 1000
>
>dove: 
>- $X_{i}$ se è 1 significa che al i-esimo lancio è uscito 5
>- $X_{i}$ se è 0 significa che al i-esimo lancio non è uscito 5
>
>$X = X_{1} + X_{2} + \dots + X_{1000}$
>
>$$
>E\left[  X \right] = \sum E[X_{i}] = n \cdot p = 1000 \cdot  \frac{1}{6}
>$$

>[!warning] prop
>
>$X = \text{Bin}(n,p) \implies E[X] = n\cdot p$
>
>>[!warning] Dim
>>ldjafhakjlhszkjlhjk
>>
>>



