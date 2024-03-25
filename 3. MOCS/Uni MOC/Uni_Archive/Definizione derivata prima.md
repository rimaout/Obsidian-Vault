---
Created: 2023-12-08
Type: Uni Note
Class:
  - "[[Calcolo Differenziale (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Derivate]]"
  - "[[Derivata prima]]"
Completed: true
---
---
# Indice
1. [[#Derivata prima di una funzione in un punto]]
	1. [[#Notazioni]]
	2. [[#Definizione]]

2. [[#Definizione Prof. Orsina]]

---
# Derivata prima di una funzione in un punto

### Notazioni:
$$ f'(x0) ~~~~;~~~~ \dot{f}(x0) ~~~~;~~~~ \frac{df}{dx}(x0) ~~~~;~~~~ D(f(x)) \vert_{x=x0} $$

---
### Definizione
>La *derivata* è il limite del [[Rapporto Incrementale]] della funzione nel punto al tendere dell'incremento a zero.

**Definizione Matematica:**
$$ f'(x0)=\lim\limits_{h\to0}{\frac{f(x0+h)-f(x0)}{h}} $$
**Definizione Geometrica:**

*Obbiettivo:* Calcolare coefficiente angolare (m) della retta tangente alla funzione f(x) nel punto x0

![[IMG_4DE80C56DCB4-1.jpeg]]


*Coefficiente angolare retta secante:*
$$ m_{sec} = \frac{\Delta y}{\Delta x} = \frac{f(x_0+h)-f(x_0)}{h} $$

*Coefficiente angolare retta tangente al punto x0:*
$$ m_{tg} = \lim\limits_{h\to0}\frac{f(x_0+h)-f(x_0)}{h} $$
- Se questo limite esiste ed è definito, la funzione $y=f(x)$ si dice derivabile nel punto di ascissa $x_{0}$

- Il valore che assume il limite si chiama *derivata di f in x_0*

---

# Definizione Prof. Orsina
$f:[a,b]\to \mathbb{R},\ \ \  x_{0}\in(a,b)$
**Rapporto incrementale di f(x):** 

$$m = \frac{f(x)-f(x_{0})}{x-x_{0}}$$
- $m$ è il coefficiente angolare della retta $\textcolor{red}{ y=f(x_{0})+m(x-xo) }$ passante per i punti $\textcolor{orange}{(xo,f(x_{0}))\ e \ (x,f(x))}$
![[IMG_324D87A74F6C-1.jpeg|300]]


**Limite rapporto incrementale:**
$$\lim_{ x \to 0 } \frac{f(x)-f(x_{0})}{x-x_{0}} $$

## Definizioni
- Sia:
	- $f:[a,b]\to\mathbb{R},\ \ \ x_{0}\in(a,b)$

- Se:
	- $\exists \lim_{ x \to x_{0} } \frac{f(x)-f(x_{0})}{x-x_{0}} = L\in \mathbb{R}$

- Allora:
$$ \begin{align}
&- \ \ f\text{ si dice \color{orange}{Derivabile}}\ in\ x_{0} \\
&- \ \ L=f(x_{0})^{'}\text{ è la \color{orange}{derivata prima }} di\ f(x)\ in\  x_{0}
\end{align}$$

---
**oss:** 

$$
\lim_{ x \to 0 }\frac{f(x) - f(x_{0})}{x - x_{0}} = \lim_{ h \to 0 }\frac{f(x_{0} + h) - f(x_{0})}{h}
$$

---