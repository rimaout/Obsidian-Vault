---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2024-10-30T15:30
updated: 2024-10-31T15:20
---
>[!abstract] Index
>1. 

>[!abstract] Related
>- 

>[!danger] TLDR

---
Se dopo il processo di individualizzazione abbiamo prodotto uno schema non in 3FN, dobbiam procedere a una fase di **decomposizione**.
Uno schema non in 3FN può essere decomposto in più modi.
R = ABC con l'insime delle dipendenza funzionali f = {A to B to C} non è in terza forma normale

R può essere decomposto in:

•R1=AB con {A to B} 
•R2=BC con {B to C}

•Oppure
	•R1=AB con {A to B} e
	•R2=AC con {A to C}
	
Entrambi gli schemi sono in 3NF, tuttavia la seconda soluzione non è soddisfacente.


Consideriamo gli schemi dele istanza appena ottenute
![[Pasted image 20241030153946.png|300]]

•L’istanza dello schema originario R che posso ricostruire da questa (l’unico modo è di ricostruirla facendo un join naturale!) è la seguente

![[Pasted image 20241030154054.png]]

•MA non è un’istanza legale di R, in quanto non soddisfa la dipendenza funzionale B to C (che sarà pure transitiva ma va soddisfatta comunque!)

**Occorre preservare TUTTE le dipendenze in F+**


sljaljòhljflò

---
## Forma Normale di Boyce-Cood

La 3NF non è la più restrittiva che si può ottenere. Ne esistono altre, tra cui la forma normale di Boyce-Codd.

>[!note] Definition
> Una relazione è in forma normale di Boyce-Codd (BCNF, Boyce-Codd Normal Form) quando in essa ogni determinante è una superchiave (ricordiamo che una chiave è anche superchiave).
>
>Una relazione che rispetta la forma normale di Boyce-Codd è anche in terza forma
normale, ma non è vero l’opposto.

>[!example] Esempio Ospedale

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
