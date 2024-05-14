---
Created: 2024-05-06
Type: Uni Note
Class:
  - "[[Calcolo Integrale (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Integrali]]"
Completed: false
---
---

>[!abstract] Index
>1. [[#Introduzione]]

>[!abstract] Related
>- [[Integrali]]
>- [[Calcolo Integrale (class)]]

---
## Introduzione

>[!info] Forma
>Integrare il rapporto tra due polinomi, esprimibile quindi con la forma generica.
>
>$$
>\int \frac{P(x)}{Q(x)}\, dx
>$$
>
>dove $P(x)$ e $Q(x)$ sono due polinomi (principalmente di grado 0, 1 o 2).

**Esistono {un numero} di possibili casi:**
1. [[#Caso Numeratore Derivata del Denominatore]]
2. [[#Caso Numeratore Costante, Denominatore 1° Grado]]

---
### Caso Numeratore Derivata del Denominatore

>[!info] Metodo
>
>$$
>\int \frac{f'(x)}{f(x)} \ dx = \ln(f( x )) +c
>$$

>[!example] Esempi
>
>$$
>\begin{align*}
>&1)\ \ \ \ \int \frac{2x}{x^{2}-5} \ dx = \ln \Big\vert x^{2}-5\Big\vert + c\\
>&2)\ \ \ \ \int \frac{x^{3}}{x^{3}+1} \ dx = \textcolor{orange}{\frac{1}{4}} \int \frac{\textcolor{orange}{4}x^{3}}{x^{3}+1}  = \frac{1}{4}\cdot  \ln \Big\vert x^{2}-5\Big\vert + c
>\end{align*}
>$$

---
### Caso Numeratore Costante, Denominatore 1° Grado

>[!info] Metodo
>1. Porte fuori la costante dal numeratore
>2. Moltiplichiamo e dividiamo per un determinato valore per ottenere la derivate del Denominatore (al numeratore)
>3. Risolvere usando metodo [[Integrali di Funzioni Razionali#Caso Numeratore Derivata del Denominatore|Numeratore Derivata del Denominatore]]
>

>[!example] Esempio
>$$
>\int \frac{\textcolor{orange}{3}}{\textcolor{lightgreen}{2}x-1} \ dx = \textcolor{orange}{3}\int \frac{1}{\textcolor{lightgreen}{2}x-1} \ dx = \frac{\textcolor{orange}{3}}{\textcolor{lightgreen}{2}}\int \frac{\textcolor{lightgreen}{2}}{\textcolor{lightgreen}{2}x-1} \ dx = \frac{\textcolor{orange}{3}}{\textcolor{lightgreen}{2}}\cdot \ln \Big\vert \textcolor{orange}{2}x-1 \Big\vert +c
>$$

>[!info] Generalizzazione
>$$
>\int \frac{k}{ax+b} \ dx = \frac{k}{a} = \frac{k}{a}\cdot \ln \Big\vert{ax+b} \Big\vert +c
>$$
>
>Dove $k$ è costanti

---
## Caso Numeratore Costante, Denominatore Quadrato

>[!note] Formula
>$$
>\int \frac{k}{\big[f( x )\big]^{2}}\ dx =\frac{k}{f'(x)} \cdot \frac{\big[f(x)\big]^{-1}}{-1}+c
>$$
>
> >[!warning]- Dimostrazione
> >$$
>>\int \frac{k}{\big[f( x )\big]^{2}}\ dx = \frac{k}{f'(x)} \cdot  \int f'(x) \cdot \big[f(x)\big]^{-2} \ dx = \frac{\big[f(x)\big]^{-1}}{-1}+c
>>$$
>>
>>Basta ricordare che:
>>- $\frac{1}{\big[f(x)^{2}\big]} = \big[f(x)^{2}\big]^{-2}$
>>- $\int f'(x) \cdot \big[f(x)\big]^{n} \ dx = \frac{\big[f( x )\big]^{n+1}}{n+1}+c$

>[!example] Esempio
>$$
>\int \frac{5}{(2x-1)^{2}} \ dx = \frac{5}{2} \int 2(2x-1)^{-2}\ dx = \frac{5}{2} \frac{(2x-1)^{-1}}{-1}+c
>$$

---
## Caso $\frac{dx+e}{ax^{2}+bx+c}$

>[!info] Metodo
>Se incontriamo integrale nella forma:
>
>$$
>\frac{dx+e}{ax^{2}+bx+c} \text{ con } \Delta<0
>$$
>
>Allora va ricondotto, facendo i dovuti rimaneggiamenti, ad integrali del tipo
>- $\int \frac{f'(x)}{1+\big[ f(x) \big]^{2}} \ dx = \text{arctg}\big[f(x)\big]+c$ 
>- $\int \frac{f'(x)}{f(x)} \ dx = \ln \big\vert f(x)\big\vert +c$ 

>[!example] Esempio
>![[Pasted image 20240512202459.png|500]]

---

## Exys

#### Caso 1
- [[#Caso Numeratore Costante, Denominatore 1° Grado]]

#### Caso 2
Se il rapporto tra polinomi è nella seguente forma (dove )

#### Caso 3
- 


#### Caso 4
- 

----

