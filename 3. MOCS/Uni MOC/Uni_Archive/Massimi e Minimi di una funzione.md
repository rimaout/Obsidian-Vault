---
Created: 2023-12-09
Type: Uni Note
Class:
  - "[[Calcolo Differenziale (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Derivate]]"
  - "[[Funzioni]]"
  - "[[Studio di Funzione]]"
Completed: false
---
---
## Index
1. [[#Massimi e Minimi relativi]]
2. [[#Massimi e Minimi assoluti]]
3. [[#Esempi]]
4. [[#Esistenza massimi e minimi]]

---
## Massimi e Minimi relativi
>[!def] Definition:
>	$f:[a,b]\to \mathbb{R}, \ \ \ \ x_{0}\in(a,b)$
>- **Massimo relativo**
>	- $x_{0}$ è un massimo relativo di f(x) se:
>	- $\exists \delta>0:\ \ \ \ f(x_{0})\geq f(x)\ \ \forall x \in[x_{0}-\delta,x_{0}+\delta]$
>- **Minimo relativo**
>	- $x_{0}$ è un minimo relativo di f(x) se:
>	- $\exists \delta>0:\ \ \ \ f(x_{0})\leq f(x)\ \ \forall x \in[x_{0}-\delta,x_{0}+\delta]$
>	

>[!danger] Teorem:
>$f:[a,b]\to \mathbb{R},\ \ \ \ x_{0}\in(a,b)$
>- Se:
>	- $x_{0}$ è un massimo/minimo relativo 
>- Allora:
>	- $f^{'}(x_{0})=0$
>	 
>![[Pasted image 20231209102954.png|500]]
>$f^{'}(1)=f^{'}(2)=0$

>[!warning] Trovare massimi e minimi relativi con lo studio di funzione della derivata 
> 1. Calcolare derivata della funzione 
> 2. Porre $f(x)^{'}\geq 0$
> 3. Effettuare studio di funzione con grafico
> ![[Pasted image 20231215174521.png|700]]

---
## Massimi e Minimi assoluti
1. Calcolare derivata $f^{'}(x)$ della funzione $f(x)$
2. Studio del segno della derivata $f^{'}(x)$
	- Trova massimi e minimi relativi
3. Calcolare funzione dei punti ottenuti dal passaggio 2 
4. Risultato:
	- I massimino relativo con il valore più alto calcolato nel passaggio 3 sarà il massimo assoluto
	- I minimo relativo con il valore più basso calcolato nel passaggio 3 sarà il minimo assolu

---
## Esempi
>[!example] Example:
>Trovare massimi e minimi relativi e assoluti della funzione $f(x)=(x-1)e^{3x}$ nel intervallo $[0,2]$
>
>*1. Calcolare derivata:*
>
>$$\begin{align}
>& f^{'}(x) = \left[ (x-1)e^{3x} \right]^{'}=\left[ x-1 \right]^{'}\cdot e^{3x} + (x-1) \cdot \left[ e^{3x}\right]^{'}=  \\
>&\ \ \ \ \ \ \ \ = 1\cdot e^{3x} +(x-1)\cdot 3\cdot e^{3x} = \\
>&\ \ \ \ \ \ \ \ = e^{3x} \cdot (1+3x-3) \\
>&\ \ \ \ \ \ \ \ = (3x-2)e^{3x}
>\end{align}$$
>
>*1. Studio di funzione di $f^{'}(x)$:*
>$$\begin{gather}
>f^{'}(x)\geq 0\\
>(3x-2)e^{3x}\geq 0\\
>3x-2\geq 0\\
>\boxed{x\geq \frac{2}{3}}
>\end{gather}$$
>
>![[Pasted image 20231215184709.png|350]]
>
>- $x = 0$ è massimo relativo
>- $x=\frac{2}{3}$ è minimo relativo
>- $x = 2$ è massimo relativo 
>
>*3. Calcolare funzione dei punti ottenuti dal passaggio 2:*
>$f(x)=(x-1)e^{3x}$ quindi:
>$$\begin{align}
>&- \ \ x=0 \to f(0)= 1 \\
>&-\ \ x=\frac{2}{3}\to f( 2 / 3)= -\frac{1}{3}\cdot e^{2} \\
>&-\ \ x=2\to f(2)= e^{6}
>\end{align}$$
>
>*4. Risultato:*
>	- I massimino relativo con il valore più alto calcolato nel passaggio 3 sarà il massimo assoluto
>	- I minimo relativo con il valore più basso calcolato nel passaggio 3 sarà il minimo assoluto
>*Quindi:*
>	- $x=\frac{2}{3}$ è il minimo assoluto
>	- $x = 2$ è il massimo assoluto

---
## Esistenza massimi e minimi
- Il [[Teorema Weierstrass]] permette di capire se esistono dei massimi e minimi. (funzione continua su intervallo chiuso)

---