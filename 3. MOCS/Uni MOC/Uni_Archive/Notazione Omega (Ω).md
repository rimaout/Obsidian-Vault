---
Created: 2024-03-06
Type: Uni Note
Class:
  - "[[Introduzione agli Algoritmi (class)]]"
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
>5. [[#Verificare g(n)]]

---
## Definizione

>[!note] Notazione Omega (Ω)
>- Rappresenta il limite inferiore o lo ==scenario migliore== del tempo di esecuzione di un algoritmo. 
>- Fornisce un limite inferiore sul tasso di crescita della complessità temporale dell'algoritmo man mano che la dimensione dell'input aumenta. 

**Esempio:**
- Se un algoritmo ha una complessità temporale di Ω(n^2), significa che il tempo di esecuzione dell'algoritmo cresce almeno quadraticamente con la dimensione dell'input.

---
## Formula

$$
\Omega(g(n)) = \{ f(n):\ \exists c>0,\  n_{0}\geq 0\ \ \ t.c.\ \ f(n) \geq c \cdot g(n)\  \forall n\geq n_{0}  \}
$$

>[!note] Ovvero
>$f(n)\in \Omega(g(n))$ 
>
>Se esistono due costanti:
>- $c>0$
>- $n_{0}\geq 0$
>
>Tali che:
>- $f(n)\geq c \cdot g(n)$    per ogni $n \geq n_{0}$

![[Pasted image 20240306164144.png|500]]

>[!warning] oss
> $\Omega(g(n))$ rappresenta l'insieme di tutte le funzioni che **dominano** dalla funzione $g(n)$

---
## Limite

Se il limite del rapporto $f(n) / g(n)$ per $n\to \infty$ è positivo o infinito allora la funzione $f(n)$ è $\Omega(g(n))$

$$
\lim_{ n \to \infty } \frac{f(n)}{g(n)} \not = 0\ \iff\ f(n)\in\Omega(g(n))
$$

---
## Calcolare g(n)



---
## Verificare g(n)

Per Verificare verificare se $f(n) \in \Omega(g(n))$ abbiamo 3 metodi:
- [[#Limite]] ovvero $\lim_{ n \to \infty } \frac{f(n)}{g(n)}\not= 0$ 
- [[#Formula]] ovvero:
	- Scrivere in forma $f(n) \leq c \cdot g(n)$ e trovare costanti $c$ e $n_{0}$ che la verificano 
- Grafico dove dopo un certo $n_{0}$ la funzione $g(n)$ è sempre più grande di $f(n)$

---