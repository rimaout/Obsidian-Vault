---
created: 2024-04-22
type: Uni Note
class:
  - "[[Calcolo Integrale (class)]]"
academic year: 2023/2024
related:
  - "[[Integrali]]"
  - "[[Calcolo Integrale (class)]]"
completed: true
updated: 2026-01-31T13:32
---
---

>[!abstract] Index
>1. [[#Integrazione per Sostituzione]]
>2. [[#Sostituzione per gli Integrali Composti]]

>[!abstract] Related
>- [[Integrali]]
>- [[Calcolo Integrale (class)]]

---
## Integrazione per Sostituzione

>[!info] Introduzione
>Alcuni integrali possono essere ricondotti ad integrali noti/integrali di funzioni elementari di cui è facile trovare la primitiva.
>
>In questi casi possiamo utilizzare il metodo dell'integrazione per sostituzione per risolverli, effettuando un cambio di variabile  andando a sostituire ogni riferimento alla variabile originale presente nell’integrale, inclusi gli estremi dell’intervallo e la variabile di integrazione.

>[!note] Metodo
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
>\frac{1}{3} \int^{12}_{3} e^{y} \, dy = \frac{e^{y}}{3} \Bigg\vert^{12}_{3} = \frac{e^{3x}}{3} \Bigg\vert^{4}_{1} = \frac{e^{12}-e^{3}}{3}
>$$

>[!example] Esempio 1
>![[Pasted image 20240508174911.png|700]]

>[!example] Esempio 2
>![[Pasted image 20240508181602.png|650]]

>[!example] Esempio 3
>![[Pasted image 20240512113517.png|800]]

---
## Sostituzione per gli Integrali Composti

>[!info] Introduzione
>Tecnica per la Risoluzione di integrali composti basata sulla formula:
>
>$$
>\int^{b}_{a} f\big( g(x) \big) \cdot  g'(x)\, dx =\int^{g(b)}_{g(a)}f(y)\ dy
>$$
>
>Vedi: [[Integrali di Funzioni Composte]]

>[!info] Metodo
>
>$\int^{b}_{a} f\big( g(x) \big) \cdot  g'(x)\, dx$
>
>**1. Calcolare nuova variabile di integrazione:**
>-  $y=g(x)$
>-  $dy = g'(x)\, dx$
>
>**2. Calcolare nuovi estremi di integrazione:**
>- $a\to g(a)$ 
>- $b \to g(b)$
>
>**3. Risolvere integrale per y:**
>- $\int^{g(b)}_{g(a)}f(y)\ dy$
>- Sostituire la $y$ del risultato dell'integrale con $g(x)$
>- Risolvere
>

>[!example] Esempio 1
>![[Pasted image 20240422173129.png|500]]

>[!example] Esempio 2
>![[Pasted image 20240422174233.png|500]]

>[!example] Esempio 3
>![[Pasted image 20240422180839.png|650]]

---