---
type: Uni Note
class:
  - "[[Automi (class)]]"
academic year: 2024/2025
related:
completed: false
created: 2025-10-20T11:16
updated: 2025-10-23T17:17
---
## Introduzione

Quando si lavora con le grammatiche context-free, può essere conveniente averle in una forma semplificata. Una di queste forme è la *Forma Normale di Chomsky*.

>[!note] Definizione: Forma Normale di Chomsky (CNF)
>
>Un CFG $G = \big( V,\Sigma,R,S \big)$ viene detto in **Chomsky's Normal Form (CNF)** se tutte le regola in $R$ assumono la una delle seguenti forme:
>- $A \to BC$
>- $A \to a$
> 
>Dove:
>- $a$ è un terminale ($a \in \Sigma$)
>- $A$ è una variabile qualsiasi ($A \in V$)
>- $B$ e $C$ sono variabile diverse dalla variabile iniziale ($B,C \in V -\{ S \}$)
>
>Inoltre permettiamo la regola $S \to \epsilon$, dove $S$ è la variabile iniziale.

## Conversione in Forma Normale di Chomsky

>[!danger] Teorema
>
>Per ogni CFG $G$, si ha che:
>
>$$
>\exists \text{CFG }\,  G' \in \text{CNF} \mid L(G) = L(G')
>$$

È possibile trasformare ogni grammatica $G$ in forma normale di Chomsky. La trasformazione consiste nel rimpiazzare le regole, che violano le condizioni di della forma normale, con regole equivalenti che sono adeguate.

>[!warning] Dimostrazione/Procedimento
>
>Dato un CFG $G = \big( V,\Sigma, R,S\big)$, costruiamo un CFG $G'$ in CNF equivalente a $G$ utilizzando il seguente procedimento:
>
>**1)** Aggiungiamo una *nuova variabile iniziale* $S_{0}$ e la regola $S_{0} \to S$
>
>**2)** Eliminiamo tutte le $\textcolor{orange}{\epsilon\text{-regole}}$ nella forma $A \to \epsilon$ dove $A \in V - \{ S_{0} \}$, per ogni regola in $R$ contenente delle occorrenze di $A$ vengono aggiunte delle regole in cui vengono eliminate tutte le possibili combinazioni di occorrenze di $A$
>- *es:* e viene rimossa $A \to \epsilon$ e in $R$ esiste $B → uAvAw\ \text{ t.c. }\ u, v, w \in (V \cup \Sigma)^{*}$, vengono aggiunte le regole $B → uvAw \mid uAvw \mid uvw$
>  
>**3)**  Eliminiamo tutte le $\textcolor{orange}{\text{regole unitarie}}$ nella forma $A \to B$, e ogni regola $B \to u$ viene sostituita da una regola $A \to u$, dove $u \in (V \cup \Sigma)^{*}$.
>
>**4)** Eliminiamo ogni regola $A \to u_{1} \dots u_{k}$ dove $k \geq 3$ e $\forall i \in [1, k]\ u_{i} \in (V \cup \Sigma)$, vengono aggiunte le variabili $A1, \dots , A_{k-2}$ e le seguenti regole:
>
>$$
>A \to u_{1}A_{1} \ \ \ \ \ A_{1} \to u_{2}A_{2} \ \ \ \dots \ \ \ A_{k-3} \to u_{k-2}A_{k-2}\ \ \ \ \ A_{k-2} \to u_{k-1}u_{k}
>$$
>
>**5)** Per ogni regola rimanente nella forma $A \to u_{1}u_{2} \in u_{1},u_{2} \in (V \cup \Sigma)$, se $u_{1} \in \Sigma$ allora viene aggiunta la variabile $U_{1} \to u$, e la regola $A \to u_{1}u_{2}$ con la regola $A \to U_{1}u_{2}$. Analogamente, lo stesso viene svolto se $u_{2} \in \Sigma$.
>
>>Poiché le operazioni svolte dall’algoritmo non modificano le stringhe generabili dalla CFG, ne segue automaticamente che $L(G) = L(G')$.

>[!example] Esempio

