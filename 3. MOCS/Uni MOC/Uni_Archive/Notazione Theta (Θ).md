---
created: 2024-03-06
type: Uni Note
class:
  - "[[Introduzione agli Algoritmi (class)]]"
academic year: 2023/2024
related:
  - "[[Analisi Asintotica degli Algoritmi]]"
completed: false
updated: 2024-05-27T13:29
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

>[!note] Notazione Theta (Θ)
>- Rappresenta ==sia il limite superiore che quello inferiore== del tempo di esecuzione di un algoritmo. 
>- Fornisce un limite preciso sul tasso di crescita della complessità temporale dell'algoritmo man mano che la dimensione dell'input aumenta.

>[!warning] oss

**Esempio:**
- Un algoritmo ha una complessità temporale di Θ(n), significa che il tempo di esecuzione dell'algoritmo cresce linearmente con la dimensione dell'input, ma né più velocemente né più lentamente.

---
## Formula

$$
\Theta(g(n)) = \{ f(n):\ \exists c_{1},c_{2}>0,\  n_{0}\geq 0\ \ \ t.c.\ \ c_{2}\cdot g(n) \leq f(n)\leq c_{1} \cdot g(n)\  \forall n\in n_{0}  \}
$$

>[!note] Ovvero
>$f(n)\in \Theta(g(n))$ 
>
>Se esistono tre costanti:
>- $c_{1}>0$
>- $c_{2}>0$
>- $n_{0}\geq 0$
>
>Tali che:
>- $c_{2}\cdot g(n) \leq f(n)\leq c_{1} \cdot g(n)$    per ogni $n \geq n_{0}$

![[Pasted image 20240306164531.png|400]]

>[!warning] oss
> $\Theta(g(n))$ rappresenta l'insieme di tutte le funzioni che hanno lo **stesso ordine asintotico** dalla funzione $g(n)$

---
## Limite
Se il limite del rapporto $f(n) / g(n)$ per $n\to \infty$ è un numero finito $k$, allora la funzione $f(n)$ è $\Theta(g(n))$

$$
\lim_{ n \to \infty } \frac{f(n)}{g(n)} = \ell \in(0, +\infty )\ \iff\ f(n) \in \Theta(g(n))
$$

dove $\ell$ è una costante compresa tra $0$ e $+\infty$ (esclusi)

---
## Calcolare g(n)



---
## Verificare g(n)
Per verificare verificare $f(n) \in \Theta(g(n))$ abbiamo 3 metodi:
- [[#Limite]] ovvero:  $\lim_{ n \to \infty } \frac{f(n)}{g(n)}= k$ 
- [[#Formula]] ovvero scrivere in forma: 
	- $f(n)\leq c_{1} \cdot g(n)$ trovare costanti $c_{1}$ e $n_{0}$ che la verificano 
	- $f(n)\geq c_{2} \cdot g(n)$ trovare costanti $c_{2}$ e $n_{0}$ che la verificano 
- Grafico dove dopo un certo $n_{0}$ la funzione $f(n)$ è sempre più grande di $g(n)$
	-  ($O$) --> $c_{1} \cdot g(n)$ sempre più grande di $f(n)$ 
	-  ($\Omega)$ --> $c_{2} \cdot g(n)$ sempre più piccolo di $f(n)$

