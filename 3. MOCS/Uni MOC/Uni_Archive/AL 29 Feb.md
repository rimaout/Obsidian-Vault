---
Created: 2024-02-29
Type: Uni Note
Class:
  - "[[Algoritmi (class)]]"
Academic Year: 2023/2024
Related: 
Completed: false
---
---

$f(n) = O(g(n))$

**Esempio:**
$\sqrt{n} = O(n)$ --> $n$ domina $\sqrt{ n }$

![[IMG_DA169AF167D0-1.jpeg|400]]


$$\begin{align}
&\exists x>0\ \ \ f(n)\leq c \cdot g(n)\ \ \forall  n>n_{0}  \\
& \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \sqrt{ n }\ \leq c\cdot n
\end{align}
$$
>[!warning] Oss:
>se esiste:
>-  $f(n)\leq c \cdot g(n)$
>
>allora: 
>- $\lim_{ n \to \infty } \frac{f(n)}{g(n)}\leq c$

>[!warning] Oss:
$f(n) = O(g(n))$ --> $\lim_{ n \to \infty } \frac{f(n)}{g(n)}\not= +\infty$

>[!example] Example:
>$\lim_{ n \to \infty \frac{\sqrt{ n }}{n}}= \lim_{ n \to \infty } \frac{\sqrt{ n }}{ \sqrt{ n } \cdot \sqrt{ n }} =\frac{1}{\sqrt{ n }}= \frac{1}{+\infty}=0$

>[!warning] Oss:
$\log n$ è sempre inferiore ad $n$


$$
\lim_{ n \to \infty } \frac{\ln n}{n} = \lim_{ n \to \infty } \frac{{[\ln n]^{'}}}{[n]^{'}} = \lim_{ n \to \infty } \frac{1 / n}{1} = 0
$$

---

$n^{2} = O(n)$ è falso ($n^{2}$ cresce più velocemente di n)

infatti:
- $n^{2} \leq c \cdot n$ $\iff$ $n \leq c$ (impossibile per $n \to \infty$)
dim: 
- $\lim_{ n \to \infty } \frac{n^{2}}{n} = \lim_{ n \to \infty } n = +\infty$ 
- per avere $n^{2} = O(n)$ il risultato deve essere compreso tra $[0, +\infty)$ 

---
>[!example] Example:
>**Trovare  O grande** di $7\sqrt{ n }+ \log n$
>- $7\sqrt{ n }+\log n$  $\leq$
>- $7\sqrt{ n }+\sqrt{ n }$  $=$
>- $8\sqrt{ n }$
>
>Trovata forma $c \cdot \sqrt{ n }$ quindi:
>- $7\sqrt{ n }+ \log n = O(\sqrt{ n })$

>[!example] Example:
>**Trovare C** di $5n=O(n)$
>- $5n\leq c\cdot n$
>- $c=5$

>[!example] Example:
>

## Upper bound $O$

>[!def] Definizione
$f(n) = O(g(n))$
>
> - $g(n)$ domina $f(n)$

**Capire se:**
Capire se $f(n) = O(g(n))$ ( ovvero $g(n)$ domina $f(n)$ )
1. $\lim_{ n \to \infty } \frac{f(n)}{g(n)}$ deve essere compreso tra $[0,+\infty)$
2. Scrivere in forma $f(n) \leq c \cdot g(n)$ e trovare costanti $c$ e $n_{0}$ che la verificano 
3. Grafico dove dopo un certo $n_{0}$ $f(n)$ è sempre più piccola di $g(n)$

**Calcolare g(n)**
- ...

## Lower bound $\Omega$ 

>[!def] Definizione
>$f(n) = \Omega (g(n))$
>- $f(n)$ domina $g(n)$

**Capire se:**
Capire se $f(n) = O(g(n))$ 
1. $\lim_{ n \to \infty } \frac{f(n)}{g(n)}$ deve essere compreso tra $(0,+\infty]$
2. Scrivere in forma $f(n) \geq c \cdot g(n)$ e trovare costanti $c$ e $n_{0}$ che la verificano 
3. Grafico dove dopo un certo $n_{0}$ la funzione $f(n)$ è sempre più grande di $g(n)$

**Calcolare g(n)**
- ...

## Limite asintotico stretto $\Theta$

>[!def] Definizione
>$f(n) = \Theta (g(n))$
>- $f(n)$ domina $g(n)$ e $g(n)$ domina $f(n)$
>
>Quindi esiste un $c_{1},\ c1$ t.c:
>- $f(n)\leq c_{1} \cdot g(n)$ ($O$)
>- $f(n)\geq c_{2} \cdot g(n)$ ($\Omega$)

**Capire se:**
Capire se $f(n) = O(g(n))$ ( ovvero $g(n)$ domina $f(n)$ )
1. $\lim_{ n \to \infty } \frac{f(n)}{g(n)}$ deve essere compreso tra $(0,+\infty)$
2. Scrivere in forma 
	- $f(n)\leq c_{1} \cdot g(n)$ trovare costanti $c_{1}$ e $n_{0}$ che la verificano 
	- $f(n)\geq c_{2} \cdot g(n)$ trovare costanti $c_{2}$ e $n_{0}$ che la verificano 
3. Grafico dove dopo un certo $n_{0}$ $f(n)$ esiste sia:
	-  $c_{1} \cdot g(n)$ sempre più grande di $f(n)$
	-  $c_{2} \cdot g(n)$ sempre più più di $f(n)$

**Calcolare g(n)**
- ...



>[!example] Example:
$$f(n) = \sum_{i=1}^{n}i = \Theta (n^{2})$$
>
>**Dimostrazione:**
>1. Dimostriamo $f(n) = O(n^{2})$
>- $S \leq c \cdot n^{2}$	
>- $S = \sum_{i=1}^{n}i$
>	- $S \leq n\sum_{i=1}^{n}i$
>	- $S \leq n\sum_{i=1}^{n}n$
>	- $S \leq n \cdot n$
>	- $S \leq n^{2}$
>
>2. Dimostriamo $f(n) = \Theta(n^{2})$

---

