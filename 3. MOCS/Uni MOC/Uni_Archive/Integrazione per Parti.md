---
Created: 2024-05-02
Type: Uni Note
Class:
  - "[[Calcolo Integrale (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Integrali]]"
Completed: true
---
---

>[!abstract] Index
>1. [[#Introduzione]]
>2. [[#Esempi]]
>3. [[#Integrare per parti due o più volte]]

>[!abstract] Related
>- [[Integrali]]
>- [[Calcolo Integrale (class)]]

---
## Introduzione

Metodo utilizzato per semplificare integrali nella forma $\int f(x)\, g'(x)\, dx$

>[!info] Formula
>Se il prodotto tra funzioni $f(x)\cdot g^{\prime}(x)$ è integrabile, allora:
>
>$$
>\int f(x)\, g'(x)\, dx\ = \ f( x )\, g(x)- \int f'(x)\, g(x)\, dx 
>$$

>[!warning] Quando utilizzarlo
> L'obbiettivo di questo metodo è quello di trasformare l’integrale originale in un’altra forma più facile da calcolare.
> 
>Ma non è assicurato la nuova forma sia più semplice dell'originale

---
## Esempi

>[!info] Esempio 1
>![[signal-2024-05-02-171324_002.png|500]]

>[!info] Esemepio 2
>![[signal-2024-05-02-171405_002.png|500]]

>[!info] Esempio 3
>![[signal-2024-05-02-171419_002.png|650]]
>In questo caso serve effettuare l'integrazione per parti più volte vedi [[#Integrare per parti due o più volte]] per altri esempi

>[!info] Esempio 4
>![[signal-2024-05-02-173430_002.png|500]]

---
## Integrare per parti due o più volte

Quando si hanno integrali di funzioni con derivate cicliche, come ad esempio $\textcolor{orange}{\int x^{\alpha}\cdot \sin (x)\,dx}$, $\textcolor{orange}{\int x^{\alpha}\cdot\cos(x)\,dx}$ e $\textcolor{orange}{\int x^{\alpha}\cdot e^{x}\,dx}$ può capitare di dover riapplicare l'integrazione per parti sul risultato dell'iterazione precedente.

>[!info] Esempio 
>![[Pasted image 20240506172201.png|700]]

---
## Integrali Ciclici

https://alem1105.github.io/Quartz/Primo-Anno/Secondo-Semestre/Calcolo-Integrale/Integrali#integrazione-per-parti-fattore-differenziale-1-e-integrali-ciclici
---
## Fattore differenziale 1

https://alem1105.github.io/Quartz/Primo-Anno/Secondo-Semestre/Calcolo-Integrale/Integrali#integrazione-per-parti-fattore-differenziale-1-e-integrali-ciclici
---


