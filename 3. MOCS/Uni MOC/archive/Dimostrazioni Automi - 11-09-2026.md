---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2026-09-11T14:16
updated: 2026-09-11T15:46
---
## $L(DFA) \subseteq L(NFA)$

banale

## $L(NFA) \subseteq L(DFA)$

Sia l' NFA $N = (Q_{N}, \Sigma^{\epsilon}, \delta_{N}, q_{0_{N}}, F_{N})$

Ora creiamo un DFA $D = (Q_{D}, \Sigma, \delta_{D}, q_{0_{D}}, F_{D})$ dove:
- $Q_{D} = {\cal P} (Q_{N})$
- $q_{0_{D}} = E\big(\{q_{0_{N}}\}\big)$
- $F_{D} = \{R \in Q_{D} \mid \exists q \in R : q \in F_{N} \}$
- $\delta_{D}(R,c) = \bigcup_{q \in R} E(\delta_{N}(q,c))$

$$
E(R) = \{q\ |\ \exists q_{_{D}} \in R \wedge  \text{è possibile raggiungere  partendo da q utilizzando soltanto epsilon archi} \} \ \ \ \text{dove R}\in Q_{D}
$$

Funziona per costruzione
## Chiusura Complemento

Dato $D$ un $DFA$ tale che $D = (Q, \Sigma, \delta, q_{0}, F)$

Definiamo la sua negazione come DFA $D_{2}$ tale che $D_{2} = (Q, \Sigma, \delta, q_{0}, F_{N})$ dove $F_{N} = Q / F$

## Chiusura Unione

Dati $N_{a}$, $N_{b}$ due DFA tali che_
- $N_{a} = (Q_{a}, \Sigma^{\epsilon}, \delta_{a}, q_{0a}, F_{a})$
- $N_{b} = (Q_{b}, \Sigma^{\epsilon}, \delta_{b}, q_{0b}, F_{b})$

Ora costuiamo $N = (Q,\Sigma^{\epsilon}, \delta, q_{0}, F$) tale che:
- $Q = Q_{a} \cup Q_{b} \cup \{q_{s}\}$
- $q_{0} = q_{s}$
- $F = F_{a} \cup F_{b}$

$$
\delta(q,c) = \begin{cases}
\delta_{a}(q,c) &\text{se } q \in Q_{a} \\
\delta_{b}(q,c) &\text{se } q \in Q_{b} \\
\{ q_{0a},q_{0b} \} &\text{se } q = q_{s}, c=\epsilon \\
\emptyset  &\text{se } q=q_{s}, c = \epsilon
\end{cases}
$$

## Chiusura Intersezione


## Chiusura Concatenazione


## Chiusura Potenza


## Chiusura Start

