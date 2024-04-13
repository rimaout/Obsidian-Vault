---
Created: 2024-03-21
Type: Uni Note
Class:
  - "[[Introduzione agli Algoritmi (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Risoluzione Equazione di Ricorrenza]]"
Completed: true
---
	---

>[!info] Index
>1. [[#Introduzione]]
>2. [[#Metodo]]
>3. [[#Esempi]]

---
## Introduzione 

Utilizzato per la [[Risoluzione Equazione di Ricorrenza|risoluzione di equazione di ricorrenza]] di [[Algoritmi Iterativi]] basati sulla ricorrenza del **dividi e impera**

>[!note] Equazione di ricorrenza 
>L'equazione di ricorrenza di questo tipo di algoritmi ha questa struttura:
>$$
>T(n) = \begin{cases}
>a\cdot \left( \frac{n}{b} \right) + f(n) & \text{if }n>1 \\
>\Theta(1) 
>\end{cases}
>$$
>
>Dove $b>1$

- Il problema di dimensione $n$ è diviso in $a$ sotto problemi di dimensione $\frac{b}{n}$ 
- $f(n)$ è il costo della funzione escluse le chiamate ricorsive 

---
## Teorema 

Un algoritmo del tipo:
$$
T(n) = \begin{cases}
a\cdot \left( \frac{n}{b} \right) + f(n) & \text{if }n>1 \\
\Theta(1) 
\end{cases}
$$
Ha 3 possibili soluzioni:

>[!note] Caso 1
>$$
>T(n) = \Theta(n^{\log_{b} (a)})\ \ \text{se}\ \ f(n) = O(n^{\log_{b} (a) -\epsilon})
>$$
>per un qualche $\epsilon >0$
>

>[!note] Caso 2
>$$
>T(n) = \Theta(n^{\log_{b} (a)}\cdot \log n)\ \ \text{se}\ \ f(n) = \Theta(n^{\log_{b} (a)})
>$$

>[!note] Caso 3
>$$
>T(n) = \Theta(f(n))
>$$
>Se:
>- $f(n) = \Omega(n^{\log_{b} (a) +\epsilon})$
>- $a\cdot f\left( \frac{a}{n} \right)\leq c\cdot f(n)$
>
>Sono entrambe vere per un qualche $\epsilon >0$ e $c>1$

**vedi condizione di regolarità**

---
## Esempi



---