---
created: 2023-05-23
type: Uni Note
class:
  - "[[Calcolo Differenziale (class)]]"
related:
  - "[[Limiti]]"
completed: true
updated: 2024-06-29T13:17
---

>[!abstract] Index
>1. [[#Definizione]]
>2. [[#Regole]]

>[!abstract] Related
>- [[Limiti]]
>- [[Calcolo Differenziale (class)]]

---
## Definizione

- L'algebra dei limiti consiste in un insieme di semplici regole che mettono in relazione il passaggio al limite con le operazioni tra funzioni.

- Tali formule permettono di ridurre il calcolo di limiti di funzioni in cui compaiono somme, differenze, moltiplicazioni e rapporti al calcolo di limiti più semplici ed il più delle volte immediati.
 
---
## Regole

>[!note] 1\) Il limite della somma è uguale alla somma dei limiti
>$$
>\lim_{ n \to x_{0} } \big(f(X) \pm g(x)\big) = \lim_{ n \to x_{0} }f(X) \pm \lim_{ n \to x_{0}} g(x)
>$$

>[!note] 2\) Il limite del prodotto di una funzione per una costante è uguale alla costante per il limite della funzione
>$$
>\lim_{ n \to x_{0} }(c\cdot f(X)) = c \cdot \lim_{ n \to x_{0}} f(x)
>$$

>[!note] 3\) Il limite del prodotto è uguale al prodotto dei limiti
>$$
>\lim_{ n \to x_{0} }(f(X) \cdot g(x)) = \Big( \lim_{ n \to x_{0} }f(X)\Big) \cdot \Big(\lim_{ n \to x_{0}} g(x) \Big)
>$$

>[!note] 4\) Il limite del rapporto è uguale al rapporto dei limiti
>$$
>\lim_{ n \to x_{0} } \frac{f(x)}{g(x)} = \frac{\lim_{ n \to x_{0}}f(x) }{\lim_{ n \to x_{0}}g(x)}
>$$
>

>[!note] 5\) Passaggio al limite per funzioni composte
>Leggi: [[Limiti di Funzioni Composte]]
>$$
>\lim_{ n \to x_{0}}g(f(X)) =g \Big( \lim_{ n \to x_{0}}f(x) \Big)
>$$


