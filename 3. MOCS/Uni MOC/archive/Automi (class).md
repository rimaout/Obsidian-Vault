---
type: "[[Uni MOC]]"
academic year: 2024/2025
created: 2025-09-24T08:15
updated: 2026-10-01T13:45
---
Risorse: [Daniele Venturi](https://corsidilaurea.uniroma1.it/it/users/danieleventuriuniroma1it), [Dispenze](https://dventuri83.github.io/projects/3_acc/)

Domande del corso: Quali sone le limitazioni intrinseche della computazione

**Argomenti:**
- *Teoria degli automi*, in particolare vedremo gli automi a stati finiti che sono il primo passo per capire modelli semplici di computazione.
- *Commutabilità*, consiste nello studio di quello che si può e non può fare con i computer. Dover per computer intendiamo il modello della macchina di Turing (modello semplificato di un computer). Vedremo che esistono problemi che nessun computer può risolvere. Esempio "stabilire se un programma (macchina di touring) termina" non può essere risolto da un computer, indipendentemente dalla risorse (alt problem).
- *Complessità*, quantificheremo le risorse necessarie (spazio e tempo) per risolvere un problema.

>[!note] Linguaggi Regolari
>1. [[Linguaggi (definizioni base)]] 🟢
>2. [[Automi Deterministici (DFA)]] 🟢
>3. [[Automi Non Deterministici (NFA)]] 🟢
>4. [[Equivalenza tra DFA e NFA]] 🟢
>5. [[Linguaggi Regolari e Chiusure]] 🔴
>6. [[Espressioni Regolari]] 🟢
>7. [[NFA Generalizzati (GNFA)]] 🟠
>8. [[Pumping Lemma]] 🟠

>[!note] Linguaggi Acontestuali
>
>- [[Grammatiche e Linguaggi Acontestuali (CFG)]] 🟢
>- [[Forma Normale di Chomsky (CNF)]] 🟢
>- [[Automi a Pila (PDA)]] 🟠 (aggiungere esempi)
>- [[Equivalenza tra PDA e CFG]]

>[!note] Calcolabilità
>
>[[Macchie di Turing]]

>[!note] Complessità
>
>[[L 21 Nov Automi]]
>[[L 26 Nov Automi]]

[[Dimostrazioni Automi - 11-09-2026]]
[[Dimostrazioni Automi - 17-09-2026]]
[[Dimostrazioni Automi - 21-09-2026]]

>[!note] Esorcizzi
>
>- [[auto-esame-set-2026]]

[[ESERCIZZI AUTOMI]]

[[AUTOMI TUTTO]]

**Forma Base:**

G:
- $S \to 1A$
- $A \to 1A \mid 0A \mid \epsilon$

**Forma Normale di Chomsky** 

G:
- $S_{0} \to S$
- $S \to  AB\mid$ 
- $A \to 1$
- $B\to BB \mid 1 \mid 0$

**Dimostrazione di Correttezza:**

Obiettivo dimostrare che la gramatica $G$ riconosce il linguaggio $1\Sigma^{*}$ dove $\Sigma = \{ 0,1 \}$.

Facciamo induzione sulla lunghezza (`n`) di una stringa `w` appartenente a $L(G)$.

- *Caso Base:* Se `n = 1` allora `w = 1`.

- *Ipotesi Induttiva:* 


Dato $A := (Q, \Sigma, \delta_{A}, q_{0_{A}}, F_{A})$ l'NFA che riconosce il linguaggio $X$ ovvero $L(A) = X$

Sia $B := (Q_{B}, \Sigma, \delta_{B}, q_{0_{B}}, F_{B})$ l'NFA che dovrà riconoscere il linguaggio $X^{R}$ ovvero $L(B) = X^{R}$ dove:
- $Q_{B} = Q_{A} \cup \{ s \}$
- $q_{0_{B}} = s$
- $F_{B} = \{ q_{0_{A}} \}$


$$
\delta_{B}(q,a) \begin{cases}
F_{A} & \text{if } q=q_{0_{B}} \wedge  a = \epsilon \\
X & \text{if } \forall q \in X \wedge  q \in \delta_{A}(p,a)
\end{cases}
$$



