---
Created: 2024-05-01
Type: Uni Note
Class:
  - "[[Introduzione agli Algoritmi (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Strutture Dati]]"
  - "[[Alberi (Struttura Dati)]]"
Completed: true
---
---

>[!abstract] Index
>1. [[#Introduzione]]
>2. [[#Completo e Quasi Completo]]
>3. [[#Caratteristiche]]
>4. [[#Tipi di Rappresentazione]]

>[!abstract] Related
>- [[Alberi (Struttura Dati)]]
>- [[Strutture Dati]]
>- [[Introduzione agli Algoritmi (class)]]

---
## Introduzione 

Un **Albero Binario** è un particolare tipo di [[Alberi (Struttura Dati)#Alberi Ordinati|Albero Ordinato]], dove ogni nodo ha al massimo due figli.

>[!info] Figlio sinistro e destro
>Essendo alberi ordinati, i due figli di ciascun nodo si distinguono in **figlio sinistro** e **figlio destro.**
>![[signal-2024-05-01-123451.png|300]]

---
## Completo e Quasi Completo

>[!info] Albero Binario Completo
>Tutti i livelli contengono il massimo numero possibile di nodi.
>![[signal-2024-05-01-122756.png|300]]

>[!info] Albero Binario Quasi Comleto
>- Tutti i livelli tranne l’ultimo contengono il massimo numero possibile di nodi .
>- L’ultimo livello è riempito completamente da sinistra verso destra solo fino ad un certo punto.
>![[signal-2024-05-01-122736.png|300]]

>[!warning] Non sono alberi quasi completi
>![[signal-2024-05-01-122654_002.png|600]]

---
## Caratteristiche

In un **Albero Binario Completo** di altezza $h$:
- Il `numeoro di foglie` è $\textcolor{orange}{2^{h}}$
- Il `numero di nodi interni` è $\sum\limits^{h-1}_{i=0}2^{i} = \textcolor{orange}{2^{h}-1}$
- il `numero totale di nodi` è $2^{h}+2^{h}-1 = \textcolor{orange}{2^{h+1}-1}$
 
>[!warning] Calcolare altezza h
>Conoscendo il numero di nodi ($n$) di un albero binario completo possiamo calcolare l'altezza ($h$)
>- **Formula:** $h = \log_{2} \frac{n+1}{2}$ 
>
>>[!info]- Dimostrazione
>>$$
>>\begin{align*}
>>&n = 2^{h+1}-1\\
>>&n+1 = 2^{n+1}\\
>>&\log_{2}(n+1) = \log_{2}(2^{n+1})\\
>>&\log_{2}(n+1) = h+1\\
>>&h = \log_{2}(n+1)-1\\
>>&h = \log_{2}(n+1)-\log_{2}(2)\\
>>&h = \log_{2} \frac{n+1}{2}
>>\end{align*}
>>$$
>
>In generale:
>- Un **albero binario completo** ha $h = \Theta(\log n)$ 
>- Un **albero binario** ha $h = \Omega(\log n)$

---
## Tipi di Rappresentazione

Descriveremo ora tre diverse rappresentazioni dell’albero binario in memoria:
- [[Memorizzazione tramite puntatori (Alberi Binari)|Memorizzazione tramite puntatori]] 🟢
- [[Rappresentazione posizionale (Alberi Binari)|Rappresentazione posizionale]] 🟢
- [[Rappresentazione tramite vettore dei padri (Alberi Binari)|Rappresentazione tramite vettore dei padri]] 🟢

**Leggi:** [[Operazioni su diverse rappresentazioni di alberi binari a confronto]] 🟢

---