---
created: 2024-05-07
type: Uni Note
class:
  - "[[Calcolo Integrale (class)]]"
academic year: 2023/2024
related:
  - "[[Integrali]]"
completed: true
updated: 2024-05-27T13:29
---
---

>[!info] Teorema
>Se $f$ è una funzione continua su l'intervallo $[a,b]$, allora:
>
>$$
>\int^{b}_{a} f(x) \, dx = F(x)\bigg\vert^{b}_{a} = F(b) - F(a)
>$$
>
>Dove $F(x)$ è una **qualsiasi** [[Primitive|primitiva]] di $f(x)$

Vedi: [[Definizione di Primitiva#Risoluzione di integrali con Primitive|Risoluzione di integrali con Primitive]]

---

## Esempi

>[!note] Esempio 1
>
>$$
>\int^{2}_{0} x^{2} \, dx = \frac{1}{3}x^{3} \bigg\vert^{2}_{0} = \frac{1}{3} \cdot 3^{2} - \frac{1}{3} \cdot 3^{0} = \frac{8}{3}
>$$
>
>Infatti:
>- $f(x)=x^{2}\implies F(x) = \frac{1}{3}x^{3}$

>[!note] Esempio 2
>$$
>\int^{8}_{2} x^{2}+5x \ dx = \frac{1}{3}x^{2} + \frac{5}{2}x^{2} \Bigg\vert^{8}_{2} = \frac{1}{3} \cdot 8^{3} + \frac{5}{2}8^{2} - \frac{1}{3} \cdot 2^{3} + \frac{5}{2}2^{2} = 318
>$$
>
>Infatti:
>- $f(x)=x^{2}\implies F(x) = \frac{1}{3}x^{3}$
>- $f(x)=5x^1\implies F(x) = \frac{5}{2}x^{2}$

