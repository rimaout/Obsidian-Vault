---
Created: 2024-04-22
Type: Uni Note
Class: 
Academic Year: 2023/2024
Related: 
Completed: false
---
---

>[!abstract] Index
>1. [[#Introduzione]]
>2. [[#Metodo]]
>3. [[#Esempi]]

>[!abstract] Related
>- [[Integrali]]
>- [[Calcolo Integrale (class)]]

---
## Introduzione

Alcuni integrali possono essere ricondotti ad integrali noti/integrali di funzioni elementari di cui è facile trovare la primitiva.

In questi casi possiamo utilizzare il metodo dell'integrazione per sostituzione per risolverli, effettuando un cambio di variabile  andando a sostituire ogni riferimento alla variabile originale presente nell’integrale, inclusi gli estremi dell’intervallo e la variabile di integrazione.

>[!note] Esempio
>L'integrale
>$$
>\int^{4}_{1} e^{3x}
>$$
>è molto simile all'integrale di $f(x)=e^{x}$  il cui risultato sappiamo essere $F(x)=e^{x}$, applichiamo il metodo della sostituzione:
>- Poniamo $y = 3x$ al fine di trasformare $f(x)=e^{3x}=e^{y}$
>- Gli estremi dell’intervallo devono essere modificati poiché quando $x = 1$ abbiamo che $y = 3\cdot1 = 3$, mentre quando $x = 4$ abbiamo che $y =3\cdot 4 =12$
>- Anche la variabile di integrazione deve essere modificata, poiché se $y = 3x$, ne segue che $y^{′} = [3x]^{′} = 3$
>
>$$
>\begin{align*}
>&y=3x\\
>&dy=[3x]^{'}dx\\
>&dy=3\ dx\\
>&\frac{{dy}}{3} = dx
>\end{align*}
>$$
>
>Dunque, una volta sostituiti tutti i riferimenti alla variabile di integrazione, l’integrale che otterremo sarà:
>$$
>\int^{4}_{1} e^{3x} \, dx = \int^{12}_{3} e^{y} \, \frac{{dy}}{3} = \frac{1}{3} \int^{12}_{3} e^{y} \, dy
>$$
>
>A questo punto, ci basterà calcolare l’integrale immediato ottenuto, per poi riportare il risultato ottenuto in termini della variabile di integrazione originale:
>
>$$
\frac{1}{3}
>$$



## Cose

>[!info] Tecnica per la Risoluzione di integrali composti basata sulla formula:
>
>$$
>\int^{b}_{a} f\big( g(x) \big) \cdot  g'(x)\, dx =\int^{g(b)}_{g(a)}f(y)\ dy
>$$

---
## Metodo

$\int^{b}_{a} f\big( g(x) \big) \cdot  g'(x)\, dx$

**1. Calcolare nuova variabile di integrazione:**
-  $y=g(x)$
-  $dy = g'(x)\, dx$

**2. Calcolare nuovi estremi di integrazione:**
- $a\to g(a)$ 
- $b \to g(b)$

**3. Risolvere integrale per y:**
- $\int^{g(b)}_{g(a)}f(y)\ dy$
- Sostituire la $y$ del risultato dell'integrale con $g(x)$
- Risolvere

---
## Esempi

>[!example] es1
>![[Pasted image 20240422173129.png|500]]

>[!example] es2
>![[Pasted image 20240422174233.png|500]]

>[!example] es3
>![[Pasted image 20240422180839.png|650]]

---