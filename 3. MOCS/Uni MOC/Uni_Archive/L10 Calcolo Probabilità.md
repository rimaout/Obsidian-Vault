---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2024-10-21T16:15
updated: 2024-10-21T18:16
---
>[!abstract] Index
>1. 

>[!abstract] Related
>- 

>[!danger] TLDR

---

## Es 9

**Link:** https://github.com/sapienzastudentsnetwork/calcolo-delle-probabilita/discussions/296

![[Pasted image 20241021161720.png]]

- $U_{A}:\ 2N, 4R$
- $U_{B}:\ 8B, 4R$
- $U_{C}:\ 1B, 3R$
  
  $E = \#\text{Estraggo B da }U_{a}$
  $F = \#\text{Estraggo 2B e 1R}$

![[Pasted image 20241021163719.png]]


**Tutti gli esercizi sono su Ipad**

---

$$
E \perp\!\!\!\!\!\!\perp F \implies E \perp\!\!\!\!\!\!\perp F^{c}
$$

- Supponiamo che $E$ e $F$ siano indipendenti
- Supponiamo che $E$ e $G$ siano indipendenti

Sapendo questo è possibile dire che $E$ è indipendente da $F \cap G$?

**No**, $E$ E $F\cap G$ possono essere **dipendenti**

>[!example] Esempio
>Si lanciano due dadi
>
>- $E = \#\text{la somma dei dati è 7}$
>- $F = \#\text{1° dado da 4}$
>- $G = \#\text{2° dado da 3}$
>  
>  Sappiamo che $E E \perp\!\!\!\!\!\!\perp F$
>  
>  devo provare che $E \perp\!\!\!\!\!\!\perp G$:
>  
>  - $P(E) = \frac{6}{36}$
>  - $P(4) = \frac{1}{6}$
>  - $P(E \cap G) = \frac{1}{26}\ \ \ \ \ \ \ \ \ \ \ \ oss: E\cap G = \{ 4,3 \}$
> 
> Ho $P(E) \cdot P(4) = \frac{1}{6} \cdot \frac{1}{6} = \frac{1}{36} = P(E\cap G)$
> 
> Quindi: $E \perp\!\!\!\!\!\!\perp G$
> - $E\ \ \not \perp\!\!\!\!\!\!\!\!\perp \ F: P(E \vert F \cap G) = 1 \not = P(E)$

>[!note] Definizione
>Dati 3 eventi $E,F,G$ si dice che sono indipendenti se:
>- $P(E\cap F) = P(E) \cdot P(F)$
>- $P(E\cap G) = P(E)\cdot P(G)$
>- $P(F \cap G) = P(F) \cdot P(G)$
>- $P(E \cap F\cap G) = P(E)\cdot P(F) \cdot P(G)$

>[!warning] Teo
>Se $E,F,G$ sono indipendenti, allora $E$ è indipendente da ogni evento costruito a partire da $F$ e$G$ usando: unione, intersezione, complementare.

>[!example] Esempio
>Se $E,F,G$ sono indipendenti allora:
>- $E \perp\!\!\!\!\!\!\perp (F\cap G)$
>- $E \perp\!\!\!\!\!\!\perp (F \cup G)$
>- $E \perp\!\!\!\!\!\!\perp (F^{c}\cap G)$
>- $E \perp\!\!\!\!\!\!\perp F^{c}$

>[!note] Definizione generalizzata
>
>Dati $n$ eventi $E_{1},\dots ,E_{n}$, questi sono detti indipendenti se:
>
>$\forall A \subset \{ 1,2,\dots,n \}$  con $A \not = \emptyset$ allora:
>
>$$
>P \big(\bigcap E_{i}) = \prod_{i\in A} P(E_{i})
>$$
