---
type: Uni Note
class:
  - "[[Algebra (class)]]"
academic year: 2024/2025
related: 
completed: false
created: 2024-10-02T18:38
updated: 2024-10-03T18:16
---
>[!abstract] Index
>1. 

>[!abstract] Related
>- 

---

## Introduzione

>[!danger] Sistema di riferimento
>- Quando si parla di vettori, prima di tutto, si deve esplicitare il sistema di riferimento.
>- In questo caso parliamo di vettori nel [[Piano Cartesiano|piano cartesiano]] che a suo volta si può identificare con l'insieme $\mathbb{R}^{2}$ delle coppie ordinate di numeri reali.

>[!note] Vettore
>Ad ogni punto del [[Piano Cartesiano|piano cartesiano]] si può associare un vettore che possiamo pensare come un segmento orientato avete come estremi:
>- L'origine del [[Piano Cartesiano|piano cartesiano]] 
>- Il punto stesso
>
>![[Pasted image 20241002190331.png|220]]

---
## Notazione

Per identificare il vettore $\vec{v}$  con la coppia ordinata $(x,y)$ delle coordinate del punto $p$, possiamo utilizzare;
$$
\vec{v} = (x,y)
$$

Dove $x$ e $y$ vengono chiamati **componenti scalari**.

>[!warning] Lunghezza del vettore
>È possibile calcolare la lunghezza chiamata **NORMA** del vettore utilizzando il Teorema di Pitagora
>
>$$
>{ \lvert \vec{v} \rvert }  = \sqrt{ x^{2} + y^{2} } 
>$$

---
## Operazioni

>[!note] Somma 
>Dati due vettori $\vec{v} = (x_{1},y_{1})$ e $\vec{w} = (x_{2},y_{2})$, la somma tra $\vec{v}$ e $\vec{w}$ è un vettore avente per componenti la somma dei componendi dei due vettori:
>
>$$
>\vec{v} + \vec{w} = (x_{1} + x_{2},\ \ y_{1} + y_{2})
>$$
>
>![[Pasted image 20241003174554.png|200]]
>
>>[!warning] Disuguaglianza Triangolare della Norma
>>La norma del vettore risultante è minore della somme delle lunghezze dei vettori operandi.
>>$$
>>{ \lvert \vec{v} + \vec{w} \rvert } \leq { \lvert \vec{v} \rvert }  + { \lvert \vec{w} \rvert }  
>>$$
>
>**oss:** questo non vale se i due vettori sono paralleli e hanno lo stesso verso\

>[!note] Moltiplicazione
>
>Dato il vettore $\vec{v = (x,y)}$ ed il numero reale $\lambda$. Il vettore $\lambda \cdot \vec{v}$ ha per componenti le componenti del vettore $\vec{v}$ moltiplicate per $\lambda$.
>
>$$
>\lambda \vec{v} = (\lambda x, \lambda y)
>$$
>
>>[!warning] Esempio
>>![[Pasted image 20241003180552.png|400]]
>
>>[!warning]  Norma del vettore risultante
>La lunghezza del vettore risultante sarà il modulo del vettore moltiplicato per $\lambda$ con segno positivo:
>>$$
>>{ \lvert \vec{v} k \rvert }  = { \lvert \vec{v} \rvert } \cdot { \lvert k \rvert }  
>>$$

