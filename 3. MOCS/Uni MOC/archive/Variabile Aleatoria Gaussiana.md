---
type: Uni Note
class: "[[Calcolo delle Probabilità (class)]]"
academic year: 2024/2025
related: 
completed: false
created: 2024-12-06T12:20
updated: 2025-03-11T10:18
---
>[!abstract] Related
>- [[Calcolo delle Probabilità (class)]]

---
## Introduzione

Una variabile aleatoria gaussiana (o normale), è una variabile aleatoria che segue una distribuzione di probabilità normale, anche nota come distribuzione gaussiana. 

Questa distribuzione è caratterizzata da una curva a campana simmetrica intorno alla media, con una probabilità maggiore di osservare valori vicini alla media e una probabilità minore di osservare valori più lontani dalla media.

La distribuzione gaussiana è completamente determinata da due parametri:
- La media ($\mu$), che rappresenta il valore centrale della distribuzione
- La varianza ($\sigma^{2}$), che rappresenta la dispersione dei valori intorno alla media

![[3. MOCS/Uni MOC/archive/attachments/Pasted image 20241207115755.png|300]]

>[!note] Definizione
>
>Una v.a. $X$ è detta gaussiana (o normale) di media $\mu \in \mathbb{R}$ e con varianza $\sigma^{2}>0$  se è una v.a. continua  con funzione di densità:
>
>$$
>f(x) = \frac{1}{\sqrt{ 2 \pi }\sigma } \cdot  e^{ \frac{-(x - \mu)^{2}}{2\sigma^{2}}}
>$$
>
>Se $\mu = 0$ e $\sigma^2= 1$ allora $X$ è detta **Gaussiana Standard** dove:
>
>$$
>f(x) = \frac{1}{\sqrt{2 \pi}} \cdot  e^{-\frac{x^{2}}{2}}
>$$

>[!note] Notazione
>Una v.a. $X$ continua gaussiana di media $\mu \in R$ con varianza $\sigma^{2}>0$ è indicata con:
>
>$$
>X = \mathcal{N} \big(\mu, \sigma^{2} \big)
>$$
>
>>***oss:*** $\mu = E[x]$ e $\sigma^{2} = \text{Var}(x)$

>[!warning] Gaussiana ben definita
>
>La v.a. gaussiana è ben definite, ovvero esiste, se $f\geq 0$ e $1 = \int^{+\infty}_{-\infty} f(x)  \, dx$

---
## Funzione di distribuzione 

Sia $X =  \mathcal{N} \big(\mu, \sigma^{2} \big)$ calcoliamo $F(x)$ ovvero $P(X)\leq x$:

$$
P(X<x) = \int_{-\infty }^{x} f(z) \, dz  = \frac{1}{\sqrt{ 2\pi }\cdot \sigma} \int^{x}_{-\infty } e^{- \frac{(z-\mu)^{2}}{2\sigma^{2}} }  \, dz
$$


>[!note] Funzione di distribuzione gaussiana standard
>
>Sia $X =  \mathcal{N} \big(0, 1 \big)$ invece di scrivere $F(x)$ scriviamo $\Phi(x)$:
>
>$$
>\Phi (X) = \frac{1}{\sqrt{ 2\pi }} \int^{x}_{-\infty }e^{-\frac{z^{2}}{z}} \, dz 
>$$
>
>Sul libro sono presenti valori di $\Phi(x)$ per $x$ maggiori di 0, se vogliamo trovare il valore negativo basta fare $\Phi(-x) = 1- \Phi(x)$.
>
>>***oss:*** $\Phi(x) = P(Z\leq x)$

>[!example] Esempio
>Sia $Z \sim \mathcal{N}(0,1)$
>
>$$
>\begin{align*}
>P(|Z|\geq 2) &= P(Z\leq -2\ \text{ o }\ Z\geq 2)\\
>&=P(Z\leq -2) + P(Z\geq 2)
>\end{align*}
>$$
>
>Abbiamo che:
>- $P(Z\leq -2) = \Phi(-2) = 1 - \Phi(2)$
>- $P(Z\geq 2) =1 - P(Z<2)= 1 - \Phi(2)$
>
>Quindi:
>$$
>P(|Z|\geq 2) = 2 \cdot  (1 - \Phi(2)) = 2 \cdot  (1 - 0.9772) = 2(0.0228) = 0.0456 = 4,56%
>$$

---
## Proposizioni

>[!note] Prop 1
>Siano $\mu \in \mathbb{R}$, $\; \sigma^{2}>0\;$ e $\;Z =  \mathcal{N} \big(0, 1 \big)$, allora:
>$$
>Y := \pm \sigma Z + \mu
>$$
>
>
>***Dove possiamo calcolare:***
>- $E[Y] = E[\sigma Z + \mu] = \sigma E[Z] + \mu = \sigma \cdot 0+ \mu = \textcolor{orange}{\mu}$
>- $\text{Var}(Y) = \text{Var}(\sigma Z+\mu) = \sigma^{2}\cdot Z\cdot\text{Var}(Z) = \sigma^{2} \cdot 1 = \textcolor{orange}{\sigma^{2}}$

>[!note] Prop 2
>
>$$
>Y = \mathcal{N} \big(\mu, \sigma^{2} \big) \implies  \frac{Y-\mu}{\sigma} = \mathcal{N} \big(0,1\big)
>$$

>[!example] Esempio
>
>Sia $Y =  \mathcal{N} \big(3,16\big)$, usando $\Phi$ calcolare $P(Y \geq 10)$
>
>Per calcolare $P(Y\geq10)$ di $Y= \mathcal{N} \big(3,16\big)$, possiamo utilizzare la proprietà data:
>
>In questo caso, abbiamo:
>- $\mu = 3$
>- $\sigma^{2} = 16$
>- $\sigma = \sqrt{ 16 } = 4$
>
>Vogliamo calcolare $P(Y\geq10)$. Per farlo, possiamo trasformare $Y$ in una variabile standardizzata $Z$, utilizzando la proprietà data:
>
>$$
>Z = \frac{Y-\mu}{\sigma} = \frac{Y-3}{4}
>$$
>
>Quindi, $P(Y\geq10)$ è equivalente a 
>$$
>P\left(Z \geq \frac{10-3}{4} \right) = P\left( Z\geq \frac{7}{4} \right) = P(Z\geq1,75)
>$$
>
>Utilizzando una tabella di distribuzione standardizzata (Z-table), possiamo trovare il valore di $P(Z\geq1,75)$. La probabilità è uguale a $1 - P(Z\leq1,75)$.
>
>Dalla tabella, troviamo che $P(Z<1,75) ≈ 0,9599$. Quindi, $P(Z\geq1,75) ≈ 1 - 0,9599 ≈ 0,0401$.
>
>Quindi, $P(Y\geq10) ≈ 0,0401$
