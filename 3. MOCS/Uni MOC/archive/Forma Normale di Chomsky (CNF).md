---
type: Uni Note
class:
  - "[[Automi (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-10-20T11:16
updated: 2025-10-26T09:51
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
>- *es:* viene rimossa $A \to \epsilon$ e in $R$ esiste $B → uAvAw\ \text{ t.c. }\ u, v, w \in (V \cup \Sigma)^{*}$, vengono aggiunte le regole $B → uvAw \mid uAvw \mid uvw$
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
>
>Consideriamo la seguente grammatica $G$ non in CNF, dove $S$ è la variabile iniziale:
>
>$$
>\begin{align*}
>G: S &\ \to\  ASA \mid aB \\
>A &\ \to\ B \mid S \\
>B &\ \to\  b \mid \epsilon \\
>\end{align*}
>$$
>
>Aggiungiamo la nuova variabile iniziale $S_{0}$ e la regola $s_{0} \to S$:
>
>$$
>\begin{align*}
>G: \textcolor{orange}{S_{0}} & \textcolor{orange}{\ \to\ S} \\
>S &\ \to\ ASA \mid aB \\
>A &\ \to\ B \mid S \\
>B &\ \to\ b \mid \epsilon \\
>\end{align*}
>$$
>
>Eliminiamo la $\epsilon\text{-regola}$ $B \to \epsilon$ :
>
>$$
>\begin{align*}
>G: S_{0} &\ \to\  S \\
>S &\ \to\ ASA \mid aB \mid \textcolor{orange}{a} \\
>A &\ \to\ B \mid S \mid \textcolor{orange}{\epsilon} \\
>B &\ \to\ b \mid \cancel\epsilon \\
>\end{align*}
>$$
>
>Eliminiamo la $\epsilon\text{-regola}$ $A \to \epsilon$ :
>
>$$
>\begin{align*}
>G: S_{0} &\ \to\  S \\
>S &\ \to\ ASA \mid aB \mid a \mid \textcolor{orange}{SA} \mid \textcolor{orange}{AS} \mid \textcolor{orange}{S}\\
>A &\ \to\ B \mid S \mid \cancel\epsilon \\
>B &\ \to\ b \\
>\end{align*}
>$$
>
>Eliminiamo la regola unitaria $S \to S$ :
>
>$$
>\begin{align*}
>G: S_{0} &\ \to\ S \\
>S &\ \to\ ASA \mid aB \mid a \mid SA \mid AS \mid \cancel{S} \\
>A &\ \to\ B \mid S \\
>B &\ \to\ b \\
>\end{align*}
>$$
>
>Eliminiamo la regola unitaria $S_{0} \to S$ :
>
>$$
>\begin{align*}
>G: S_{0} &\ \to\  \cancel{S} \mid ASA \mid aB \mid a \mid SA \mid AS  \\
>S &\ \to\ ASA \mid aB \mid a \mid SA \mid AS \\
>A &\ \to\ B \mid S \\
>B &\ \to\ b \\
>\end{align*}
>$$
>
>Eliminiamo le regole unitarie $A \to B$, $A \to S$:
>
>$$
>\begin{align*}
>G: S_{0} &\ \to\ ASA \mid aB \mid a \mid SA \mid AS  \\
>S &\ \to\ ASA \mid aB \mid a \mid SA \mid AS \\
>A &\ \to\ \cancel{B} \mid \cancel{S} \mid \textcolor{orange}{b} \mid \textcolor{orange}{ASA} \mid \textcolor{orange}{aB} \mid \textcolor{orange}{a} \mid \textcolor{orange}{SA} \mid \textcolor{orange}{AS} \\
>B &\ \to\ b \\
>\end{align*}
>$$
>
>Separiamo ogni regola con tre o più elementi a destra in regole con massimo due elementi a destra:
>
>$$
>\begin{align*}
>G: S_{0} &\ \to\  \cancel{ASA} \mid \textcolor{orange}{AA_{1}} \mid aB \mid a \mid SA \mid AS  \\
>S &\ \to\ \cancel{ASA} \mid \textcolor{orange}{AA_{1}} \mid aB \mid a \mid SA \mid AS \\
>A &\ \to\ b \mid \cancel{ASA} \mid \textcolor{orange}{AA_{1}} \mid aB \mid a \mid SA \mid AS \\
>\textcolor{orange}{A_{1}} & \textcolor{orange}{\ \to\ SA} \\
>B &\ \to\ b \\
>\end{align*}
>$$
>
>
>Infine, convertiamo tutte le regole aventi due elementi a destra di cui almeno uno è un terminale:
>
>$$
>\begin{align*}
>G: S_{0} &\ \to\ AA_{1} \mid \cancel{aB} \mid \textcolor{orange}{UB} \mid a \mid SA \mid AS  \\
>S &\ \to\ AA_{1} \mid \cancel{aB} \mid \textcolor{orange}{UB} \mid a \mid SA \mid AS \\
>A &\ \to\ b \mid AA_{1} \mid \cancel{aB} \mid \textcolor{orange}{UB} \mid a \mid SA \mid AS \\
>A_{1} &\ \to\ SA \\
>\textcolor{orange}{U} &\ \textcolor{orange}{\to\  a}\\
>B &\ \to\ b \\
>\end{align*}
>$$
>
>La grammatica finale ottenuta risulta sia equivalente a quella iniziale sia in forma normale di Chomsky:
>
>$$
>\begin{align*}
>G: S_{0} &\ \to\  AA_{1} \mid UB \mid a \mid SA \mid AS  \\
>S &\ \to\ AA_{1} \mid UB \mid a \mid SA \mid AS \\
>A &\ \to\ b \mid AA_{1} \mid UB \mid a \mid SA \mid AS \\
>A_{1} &\ \to\ SA \\
>U &\ \to\ a\\
>B &\ \to\ b \\
>\end{align*}
>$$
