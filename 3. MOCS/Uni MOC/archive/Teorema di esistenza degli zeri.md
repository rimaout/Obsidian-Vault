---
created: 2023-11-20
type: Uni Note
class:
  - "[[Calcolo Differenziale (class)]]"
academic year: 2023/2024
related:
  - "[[Funzioni Continue]]"
completed: true
updated: 2024-06-29T13:35
---

>[!abstract] Index
>1. [[#Teorema]]
>2. [[#Dimostrazione]]

>[!abstract] Related
>- [[Funzioni Continue]]
>- [[Funzioni]]
>- [[Calcolo Differenziale (class)]]

---
## Teorema

>[!note] Enunciato
>Sia: 
>- $f: [a,b] \to \mathbb{R}$ continua in  $[a,b]$
>- $f(a)>0$, $f(b)<0$ ( o viceversa)
>
>Allora: 
>- $\exists c \in(a,b)\ t.c.\ \boxed{f(c)=0}$

>[!warning] Grafico
>![[Screenshot 2023-12-06 at 18.52.46.png|500]]
>![[Screenshot 2023-12-06 at 18.53.54.png|600]]

---
## Dimostrazione

- $f(a)<0$
- $f(b)>0$

1. prendo punto medio dell'intervallo $c = \frac{a+b}{2}$
2. Calcoliamo f(c) ora abbiamo tre possibili risultati 
	1. $f(c)>0$:
		- poniamo: a, b = a,  c
		- calcoliamo nuova c = $\frac{a+b}{2}$
	2. $f(c) < 0$:
		- Poniamo: a, b = c,  b
		- Calcoliamo nuova c = $\frac{a+b}{2}$
	3. $f(c) = 0$:
		- trovato 

>**oss:** questa dimostrazione è un algoritmo 