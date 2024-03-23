---
Created: 2024-03-06
Type: Uni Note
Class:
  - "[[Algoritmi 1 (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Analisi Asintotica degli Algoritmi]]"
Completed: false
---
---

>[!info] Index
>1. [[#Definizione]]
>2. [[#Formula]]
>3. [[#Limite]]
>4. [[#Calcolare g(n)]]
>5. [[Flip Flop]]

---
## Definizione

>[!note] Notazione Big O
>- Rappresenta il limite superiore o lo ==scenario peggiore== del tempo di esecuzione di un algoritmo. 
>- Fornisce un limite superiore sul tasso di crescita della complessità temporale dell'algoritmo man mano che la dimensione dell'input aumenta. 

>[!warning] oss
>Calcolare il limite superiore di un algoritmo ci permette di scoprire il costo che l'algoritmo non supererà mai

**Esempio:**
- Un algoritmo ha una complessità temporale di O(n), significa che il tempo di esecuzione dell'algoritmo cresce linearmente con la dimensione dell'input.

---
## Formula

$$
O(g(n)) = \{ f(n):\ \exists c>0,\  n_{0}\geq 0\ \ \ t.c.\ \ f(n)\leq c \cdot g(n)\  \forall n \geq n_{0}  \}
$$

>[!note] Ovvero
>$f(n)\in O(g(n))$ 
>
>Se esistono due costanti:
>- $c>0$
>- $n_{0}\geq 0$
>
>Tali che:
>- $f(n)\leq c \cdot g(n)$    per ogni $n \geq n_{0}$

![[Pasted image 20240306163855.png|500]]

>[!warning] oss
> $O(g(n))$ rappresenta l'insieme di tutte le funzioni **dominate** dalla funzione $g(n)$

---
## Limite

Se il limite del rapporto $f(n) / g(n)$ per $n\to +\infty$ è diverso da $+\infty$ allora la funzione $f(n)$ è $O(g(n))$

$$
\lim_{ n \to \infty } \frac{f(n)}{g(n)} \not = +\infty\ \iff\ f(n) \in O(g(n))
$$
---
## Calcolare g(n)



---
## Verificare g(n)

Per verificare verificare $f(n) \in O(g(n))$ abbiamo 3 metodi:
- [[#Limite]] ovvero:  $\lim_{ n \to \infty } \frac{f(n)}{g(n)}\not= +\infty$ 
- [[#Formula]] ovvero: Scrivere in forma $f(n) \leq c \cdot g(n)$ e trovare costanti $c$ e $n_{0}$ che la verificano 
- Grafico dove dopo un certo $n_{0}$ la funzione $g(n)$ è sempre più grande di $f(n)$

