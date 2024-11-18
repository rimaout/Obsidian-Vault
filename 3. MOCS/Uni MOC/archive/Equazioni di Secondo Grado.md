---
created: 2023-05-16
type: Uni Note
class:
  - "[[Matematica 0 (class)]]"
related:
  - "[[Disequazioni]]"
  - "[[Equazioni di Secondo Grado]]"
completed: true
updated: 2024-05-27T13:29
---
---
## Indice
1. [[#Definizione]]
2. [[#Numero di soluzioni]]
3. [[#Metodi risolutivi]]
	-  [[#Complete (formula $ Delta$)|Complete]]
	-  [[#Monomie]]
	-  [[#Pure]]
	-  [[#Spurie]]

---
## Definizione
Un equazione di secondo grado è un equazione in cui almeno una delle incognite è di grado 2

$$ax^2+bx+c=0$$
- `a`: coefficiente del termine di 2° grado
- `b`: coefficiente del termine di 1° grado
- `c`: coefficiente del termine di grado 0

---
## Numero di soluzioni 
- **2 Soluzioni Reali:** $\Delta > 0$ 
- **1 Soluzione Reale:** $\Delta = 0$  (due soluzioni coincidenti) 
- **0 Soluzioni Reali:** $\Delta < 0$

---
## Metodi risolutivi

### Complete (formula $\Delta$)
**Definizione:** Equazione in forma normale in cui tutti i coefficienti sono diversi da zero 

$$ax^2 + b^x +c=0\ con\ a,b,c\not =0$$
**Risultato:**

$$
x_{1,2} = \frac{-b\pm \sqrt{b^2-4ac}}{2a}\to \begin{cases}
x_{1} =\frac{-b+ \sqrt{b^2-4ac}}{2a} \\
x_{2}=\frac{-b- \sqrt{b^2-4ac}}{2a}
\end{cases}
$$

---
### Monomie
**Definizione:** Equazione in forma normale in cui tutti i coefficienti dei termini di grado 1 e 0 sono nulli ($b,c=0$)

$$ax^2 =0$$

**Risultato:**

$$x_{1,2} = 0$$

**Dimostrazione:** 

$$x_{1,2} = \frac{-b\pm \sqrt{b^2-4ac}}{2a} = \frac{-0\pm \sqrt{0^2-4\cdot a\cdot 0}}{2a}=\frac{0\pm 0}{2a}=0$$

---
### Pure

**Definizione:** 
- Equazione in forma normale in cui tutti i coefficienti dei termini di grado 1 sono nulli e il termine noto è diverso da zero ($b=0,c \not=0$)

$$ax^2 +c=0\ \ con\ a \not =0,\ c \not =0$$
**Risultato:**

$$x_{1,2} = \pm \sqrt{\frac{-c}{a} }$$

---
### Spurie

**Definizione:** 
- Equazione in forma normale in cui tutti i coefficienti dei termini di grado 1 e 0 sono nulli ($b,c=0$)

$$ax^2 + bx =0\ \ con\ \ a,b\not = 0 $$

**Risultato:**

$$x_{1} = 0,\ \ x_{2}= \frac{-b}{a}$$

**Dimostrazione:** 

$$
\begin{align}
& ax^2 + bx =0\to x(ax+b)=0 \\
&  \\
& x = 0 \\
& ax+b=0\to ax = -b\to x=\frac{-b}{a}
\end{align}
$$

---