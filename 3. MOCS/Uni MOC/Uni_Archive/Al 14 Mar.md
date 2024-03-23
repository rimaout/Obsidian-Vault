---
Created: 2024-03-14
Type: Uni Note
Class:
  - "[[Algoritmi 1 (class)]]"
Academic Year: 2023/2024
Related: 
Completed: false
---
---

>[!info] Index
>1. [[#Metodo Iterativo]]
>2. [[#Metodo dell'Albero]]
>3. [[#Teorema Principale (master theorem)]]
<4. [[#Metodo di Sostituzione]]

---
## Metodo Iterativo

>[!note] **Risolvere:** $T(n) = T(n-1)+\Theta(1)$
>- utilizza sommatorie 
>
>**Passaggi:**
>- $T(n) = T(n-1)+\Theta(1)$
>- $T(n) = T(n-2)+\Theta(1)+\Theta(1)$
>- $T(n) = T(n-3)+\Theta(1)+\Theta(1)+\Theta(1)$
>- ...
>
>Dopo un pò di iterazioni riesco a capire che: $T(n)=T(n-i)+i\cdot \Theta(1)$ dove $i$ è l'iterazione 
>
>Quindi dopo $n$ iterazioni:
>- $T(n) = T(n-n)+n\cdot \Theta(1) = n\cdot \Theta(1) = \Theta(n )$
>

>[!note] **Risolvere:** $T(n) = T(n-1)+\Theta(n)$
>
>**Passaggi:**
>- $T(n) = T(n-1)+\Theta(n)$
>- $T(n) = T(n-2)+\Theta(n)+\Theta(n)$
>- $T(n) = T(n-3)+\Theta(n-2)+\Theta(n-1)+\Theta(n)$
>- ...
>
>Dopo un pò di iterazioni riesco a capire che: $T(n)=T(n-i)+ \sum^{i}_{j=0}\Theta(n-j)$ dove $i$ è l'iterazione
>
>Quindi dopo $n$ iterazioni:
>- $T(n) = T(n-n)+\sum_{j= 0}^{n}(n-j) = \Theta(0) + \sum_{j= 0}^{n}(n-j)$
>
>>[!warning] oss
>>$\sum_{j= 0}^{n}(n-j)$  =  $n+(n-1)+(n-2)+\dots+0$ 
>
>Questa sommatoria è uguale a:
>- $\sum_{i= 0}^{n}i$  =  $0 + 1 + 2 + \dots +(n-1) + n$
>
>Quindi:
>- $T(n) =\sum_{j= 0}^{n}(n-j) = \sum_{i= 0}^{n}i$
>
>Dove:
>- $T(n) = \sum_{i= 0}^{n}i = \frac{n(n-1)}{2} = \Theta\left( \frac{n^{2}}{2} \right)= \Theta(n^{2})$

>[!note] **Risolvere** $T(n) = T(n-1)+\Theta (\ln n)$
>
>**Passaggi:**
>- $T(n) = T(n-1)+\Theta(\ln n)$
>- $T(n) = T(n-2)+\Theta(n-1)+\Theta(\ln n)$
>- $T(n) = T(n-3)+\Theta(n-2)+\Theta(\ln n-1)+\Theta(n)$
>- ...
>
>Dopo un pò di iterazioni riesco a capire che: $T(n)=T(n-i)+ \sum^{i-1}_{j=0}\ln(n-j)$ dove $i$ è l'iterazione
>
>Quindi dopo $n$ iterazioni:
>- $T(n) = T(n-n)+\sum_{j= 0}^{n}(n-j) = \Theta(1) + \sum_{j= 0}^{i}(n-j)$

>[!note] **Risolvere** $T(n) = T\left( \frac{n}{2} \right)+\Theta (1)$ Ricerca binaria
>
>oss: $T(0)=\Theta(1)$
>
>**Passaggi:**
>- $T(n) = T\left( \frac{n}{2} \right)+\Theta(1)$
>- $T(n) = T\left( \frac{n}{4} \right)+ \Theta(1)+ \Theta(1)$
>- $T(n) = T\left( \frac{n}{8} \right)+ \Theta(1)+ \Theta(1)+\Theta(1)$
>- ...
>
>Dopo un pò di iterazioni riesco a capire che: $T(n)=T\left( \frac{n}{2^{i}} \right)+ i\cdot \Theta(1)$ dove $i$ è l'iterazione
>
>Quindi dopo $n$ iterazioni:
>- $\frac{n}{2^{i}}=1$ 
>- $n=2^{i}$
>- $\log_{2}n = \log_{2}2^{i}$
>- $i = \log_{2} n$
>
>Quindi $T(n) = \Theta(\log n)$
>Dopo un pò di iterazioni riesco a capire che: $T(n)= 2^{i} \cdot T\left( \frac{n}{2^{i}} \right) +i\cdot \Theta(1)$
>Per $i=\log n$
>
>Quindi dopo $n$ iterazioni:
>- $T(n)= 2^{i} \cdot T\left( \frac{n}{2^{i}} \right) +i\cdot \Theta(1)$ 
>
>Quindi $T(n) = \Theta(\log n)$

---
## Metodo dell'Albero

>[!note] **Risolvere** $T(n) = T\left( \frac{n}{2} \right)+\Theta (1)$ Ricerca binaria

---
## Teorema Principale (master theorem)


---
## Metodo di Sostituzione


---