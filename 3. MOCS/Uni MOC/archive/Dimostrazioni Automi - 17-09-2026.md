---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2026-09-17T15:31
updated: 2026-09-17T16:45
---
## DFA = NFA

**Prima parte** - $L(DFA) \subseteq L(NFA)$ non serve dimostralo dato che per come è definito il NFA non è altro che un estensione del DFA.

**Seconda parte** - $L(NFA) \subseteq L(DFA)$ obbiettivo dimostrare che esiste u nalgoritmo per convertire un NDA in un DFA:

Sia $N := (Q_{N},\Sigma^{\epsilon},\delta_{N},q_{0_{N}},F_{N})$ l'$NFA$ da convertire. Costruiamo $D$ un $DFA$ tale che $D := (Q_{D}, \Sigma, \delta_{D}, q_{0_{D}}, F_{D})$ dove:
- $Q_{D} = {\cal P} (Q_{N})$
- $q_{0_{D}} = E(\{ q_{0_{N}} \})$
- $F_{D} = \{ R \in Q_{D} \mid R \cap F_{D} \neq 0 \}$
- $\delta_{D}(R,a) = \bigcup_{q \in R}E(\delta_{N}(q,a))$

$$
E(R) = \text{L'insieme di tutti i possibili stati che è possibile raggingere partendo R utilando solo epslilon archi, R compreso con R}\in Q_{D}
$$

## Chiusura dell'Unione su REG

Dati $L_a,L_b \in \text{REG}$ dimostriamo che se $L = L_{a} \cup L_{b}$ allora $L \in \text{REG}$.

Siano $N_{a} := (Q_{a},\Sigma,\delta_{a},q_{0_{a}}, F_{a})$ e $N_{b} := (Q_{b},\Sigma,\delta_{b},q_{0_{b}}, F_{b})$ degli $NFA$ tali che $L(N_{a}) = L_{a}$ e $L(N_{b}) = L_{b}$ ora costruiamo $N$ tale che $L(N) = L$.

Quindi sia $N := (Q, \Sigma, \delta, q_{0},F)$ dove:
- $Q = Q_{a} \cup Q_{b} \cup \{ q_{s} \}$
-  $q_{0} =q_{s}$
- $F = F_{a} \cup F_{b}$
$$\delta(q,c) = \begin{cases}
\delta_{a}(q,c) & \text{if } q \in Q_{a}\\
\delta_{b}(q,c) & \text{if } q \in Q_{b} \\
\{ q_{0_{a}},q_{0_{b}} \}
 & \text{if } q = q_{0} \wedge a = \epsilon \\
 \emptyset
 & \text{if } q = q_{0} \wedge a \not = \epsilon
 
 \end{cases}$$ 

## Chiusura dell'Intersezione su REG

Dati $L_a,L_b \in \text{REG}$ dimostriamo che se $L = L_{a} \cap L_{b}$ allora $L \in \text{REG}$.

Siano $D_{a} := (Q_{a},\Sigma,\delta_{a},q_{0_{a}}, F_{a})$ e $D_{b} := (Q_{b},\Sigma,\delta_{b},q_{0_{b}}, F_{b})$ degli $DFA$ tali che $L(N_{a}) = L_{a}$ e $L(N_{b}) = L_{b}$ ora costruiamo $D$ tale che $L(N) = L$.

Quindi sia $D := (Q, \Sigma, \delta, q_{0},F)$ dove:
- $Q = Q_{a} \times Q_{b}$
- $q_{0} = (q_{0_{a}},q_{0_{b}})$
- $F = \{ (q_{a},q_{b}) : q_{a} \in F_{A} \wedge q_{b} \in F_{B} \}$
- $\delta((q_a,q_b),c) = (\delta_{a}(q_{a},c),\delta_{b}(q_{b},c))$




