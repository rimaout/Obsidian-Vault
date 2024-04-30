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