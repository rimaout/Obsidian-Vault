---
created: 2024-05-17
type: Uni Note
class:
  - "[[Calcolo Integrale (class)]]"
academic year: 2023/2024
related:
  - "[[Calcolo Integrale (class)]]"
  - "[[Integrali]]"
  - "[[Integrali di Funzioni Razionali]]"
completed: true
updated: 2024-05-27T13:29
---
---

>[!abstract] Index
>1. [[#Caso Numeratore Derivata del Denominatore]]
>2. [[#Caso Numeratore Costante, Denominatore 1° Grado]]
>3. [[#Caso Numeratore Costante, Denominatore Quadrato]]
>4. [[#Caso $ frac{dx+e}{ax {2}+bx+c}$|Caso {dx+e} / {ax {2}+bx+c}]]

>[!abstract] Related
>- [[Calcolo Integrale (class)]]
>- [[Integrali di Funzioni Razionali]]
>- [[Integrali]]

---
## Caso Numeratore Derivata del Denominatore

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
>&2)\ \ \ \ \int \frac{x^{3}}{x^{3}+1} \ dx = \textcolor{orange}{\frac{1}{4}} \int \frac{\textcolor{orange}{4}x^{3}}{x^{4}+1}  = \frac{1}{4}\cdot  \ln \Big\vert x^{4}-1\Big\vert + c
>\end{align*}
>$$

---

## Caso Numeratore Costante, Denominatore 1° Grado

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
>Dove $k,\, a$ e $b$ sono delle costanti.

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
## Caso Numeratore Costante, Denominatore 2° Grado

>[!info] Formula
>Se incontriamo integrale nella forma:
>
>$$
>\int \frac{k}{ax^{2}+bx+c} \, dx  \text{ con } \Delta<0
>$$
>
>Allora:
>$$
>\int \frac{k}{ax^{2}+bx+c} \, dx = \frac{2k\cdot \arctan\left( \frac{2ax+b}{\sqrt{ -\Delta }} \right)}{\sqrt{ -\Delta }}
>$$

>[!example] Esempio
>![[Pasted image 20240523105357.png|700]]

---
## Caso Numeratore 1°, Denominatore 2° Grado

>[!info] Metodo
>Se incontriamo integrale nella forma:
>
>$$
>\int  \frac{dx+e}{ax^{2}+bx+c} \, dx \text{ con } \Delta<0
>$$
>
>Questi integrali vanno ricondotto, facendo i dovuti rimaneggiamenti, ad integrali del tipo:
>- $\int \frac{f'(x)}{1+\big[ f(x) \big]^{2}} \ dx = \text{arctg}\big[f(x)\big]+c$ 
>- $\int \frac{f'(x)}{f(x)} \ dx = \ln \big\vert f(x)\big\vert +c$ 

>[!example] Esempio 1
>![[Pasted image 20240512202459.png|500]]

>[!example] Esempio 2
>![[Pasted image 20240517094048.png|700]]
