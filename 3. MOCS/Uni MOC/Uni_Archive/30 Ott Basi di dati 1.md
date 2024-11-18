---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2024-10-30T15:30
updated: 2024-11-16T16:36
---

---

---
## Come calcolare $X^{+}$

**Condizione di fermata:** quando $S$ è completamente contenuto in $Z$.

dkjlshjlashl
dfljksalkj

![[Pasted image 20241031133956.png|500]]

>[!example] Esempio

>[!warning] oss
>Una chiusura non può essere vuota infatti riflessività non esiste una chiusura di attributi vuota.

>[!warning] Teorema
>Teorema: L’Algoritmo "$\text{Calcolo di }X^+$ calcola correttamente la chiusura di un insieme di attributi $X$ rispetto ad un insieme $F$ di dipendenze funzionali.
>
>**Dimostrazione:**
>Indichiamo con $Z^{(0)}$ il valore iniziale di $Z$ ($Z^{(0)} = X$) e con $Z^{i}$ ed $S^{(i)}$ ($i\geq 1$) i valori di $Z$ ed $S$ dopo l’i-esima esecuzione del corpo del ciclo; è facile vedere che $Z^{(i)}\subseteq Z^{(i+1)}$ per ogni $i$.

>[!warning] Teorema 
>$$
>A \in Z^{(j)} \implies  A \in X^{+}
>$$
>
>**Dimostrazione per induzione:**
>$Z^{finale} = X^{+}_{F}$
>$Z^{finale} \subseteq X^{+}_{F} \wedge X^{+}_{F} \subseteq Z^{finale}$
>
>$A \in Z^{finale} \Leftrightarrow  A \in X^{+}_{F}$
>
>il posso dell'induzione è basato sulle iterazioni del ciclo while
>
>Caso base: $Z^{0}=x\ \ \ \ \ X \subseteq X^{+} \implies Z^{0} \subseteq X^{+}$
>
>Ipotesi induttiva: $Z^{i-1} \subseteq X^{+}_{F} \implies x \to Z^{(i-1)}\in F^{A}$
>
>Passo induttivo: $Z^{i}??$
>>*oss:* $A \in Z^{i}-Z^{i-1}$ questo significa che ha non era presente in $Z^{i-1}$ ma è presente in $Z^{i}$
>
>$A \in Z^{i}-Z^{i-1} \implies \exists y \to W \in F\ t.c.\ \textcolor{orange}{y \subseteq Z^{i-1}} \wedge A \in W$
>
>>oss: $\textcolor{orange}{y \subseteq Z^{i-1}} \underset{decomp}\implies X \to y \in F^{A} \underset{trans}\implies X \to W \in F^{A} \implies x \to A \in F^{A} \to A \in X^{+}_{F}$ 

 
>[!warning] Dimostrazione inversa
>$$
>A \in X^{+} \implies A \in Z^{(G)}
>$$
>
>**Dimostrazione per induzione:**
>$Z^{finale} = X^{+}_{F}$
>$Z^{finale} \subseteq X^{+}_{F} \wedge X^{+}_{F} \subseteq Z^{finale}$
>
>$A \in Z^{finale} \Leftrightarrow  A \in X^{+}_{F}$
>

>[!example] Example:
>$R = (A,B,C,D,E,H$
>$F = \{ AB \to CD, EH \to D, D \to H \}$
>
