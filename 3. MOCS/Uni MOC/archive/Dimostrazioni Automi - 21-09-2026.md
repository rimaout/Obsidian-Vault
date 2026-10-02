---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2026-09-21T15:02
updated: 2026-09-22T17:00
---
## Dimostrazione DFA = NFA

## Dimostrazione Chiusure su REG
- Unione
- Intersezione
- Complemento
- Concatenazione
- Star
- Plus

## Dimostrazione ${\cal L} (re) = REG$

>[!note] ${\cal L} (re) \subseteq REG$

>[!note] $REG \subseteq {\cal L} (re)$

## Dimostrazione GNFA = re

boh non ho capito bene, forse non c'è dimostrazione ma un algoritmo 

## Dimostrazione Unione tra CFG $\bigcup_{i\in[k]} L(G_{i}) = L(G)$

Sia $G_{i} = (V_{i}, \Sigma_{i}, R_{i}, S_{i})$ dei CFG dove $i \in [1,n]$ creare che esiste un GFG $G = (V, \Sigma, R,S)$ tale che $L(G) = \bigcup_{i\in [k]} L(G_{i})$.

Quindi definiamo:
- $V = \bigcup_{i \in [k]} V_{i} \cup \{ S \}$, dove per non perdere generalità si deve avere che ogni v in V sia diversa dalle altre
- $T = \bigcup_{i \in [k]} T_{i}$
- $R = \bigcup_{i \in [k]} R_{i} \cup \{ S \to S_{i} \}$ 

**Dimostrazione** - DA FARE (sembra troppo banale quindi non mi piace)
## Trasformare un DFA in un CFG

Fai un esercizio (in futuro)
## Forma Normale di Chomsky





## 