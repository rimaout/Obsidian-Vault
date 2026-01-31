---
created: 2023-11-20
type: Uni Note
class:
  - "[[Calcolo Differenziale (class)]]"
academic year: 2023/2024
related:
  - "[[Teoremi valori intermedi + Weierstrass]]"
completed: true
updated: 2026-01-31T13:32
---
---
## Index
1. [[#Enunciato 1.0]]
2. [[#Enunciato 2.0]]
3. [[#Teorema generalizzato]]

---
## Enunciato 1.0
- Sia:
	- $f: [a,b] \to \mathbb{R}\ \text{ continua su } [a,b]$
	- $t\in \mathbb{R}:\ \  f(a)\leq t\leq f(b)$ 
- Allora:
	- $\exists x_{t}\in (a,b):\ \ \boxed{f(x_{t})=t}$
	
**Quindi:** se $f:[a,b]$ è continua allora assume tutti i valori compresi tra $f(a)$ e $f(b)$

![[valorintermedi2.png|600]]

---
## Enunciato 2.0
- Sia:
	- $f:[a,b] \to \mathbb{R}\ \ \text{continua}$ si $[a,b]$

- Allora:
	- $f([a,b])=[m,M]$

- Dove: 
	 - $m = min(\{f(x),\ x \in [a,b]\})$
	 - $M = max(\{f(x),\ x \in [a,b]\})$

**Quindi:** se $f:[a,b]$ è continua allora assume tutti i valori compresi tra $f(m)$ e $f(M)$

![[valorintermedi1.png|600]]

---
## Teorema generalizzato
$f: \mathbb{R}\to \mathbb{R}$ è continua

- Se:
	- $\lim_{ x \to +\infty }f(x) = \pm \infty$
	- $\lim_{ x \to -\infty }f(x) = \mp \infty$
  
- Allora: 
	- $f(\mathbb{R}) = \mathbb{R}\ \ \ \textcolor{orange}{(\text{ surriettiva })}$

---
