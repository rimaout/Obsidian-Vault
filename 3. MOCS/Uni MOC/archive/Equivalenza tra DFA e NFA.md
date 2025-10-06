---
type: Uni Note
class:
  - "[[Automi (class)]]"
academic year: 2024/2025
related:
completed: false
created: 2025-10-03T14:14
updated: 2025-10-03T14:33
---
## Teorema

Vedremo che gli automi a stati finiti deterministici e quelli non deterministici riconoscono la stessa classe di linguaggi. Questo è estremamente utile perché a volte è molo più semplice descrivere un NFA che un DFA per un dato linguaggio.

>[!danger] Teorema: Equivalenza tra NFA e DFA
>
>Date le due classi dei linguaggi $\mathcal{L}(DFA)$ e $\mathcal{L}(NFA)$, si ha che:
>
>$$
>\mathcal{L}(DFA) = \mathcal{L}(NFA)
>$$
>
>Dove dato un alfabeto $\Sigma$, definiamo:
>- La classe dei linguaggi di $\Sigma$ riconosciuti da un NFA il come: $\mathcal{L}(NFA) = \big\{\mathcal{L} \subseteq \Sigma^{*}\ |\ \exists\; \text{NFA}\ N \text{ t.c } \mathcal{L}= \mathcal{L}(N)\big\}$
>- La classe dei linguaggi di $\Sigma$ riconosciuti da un DFA il come: $\mathcal{L}(DFA) = \big\{\mathcal{L} \subseteq \Sigma^{*}\ |\ \exists\; \text{DFA}\ D \text{ t.c } \mathcal{L}= \mathcal{L}(D)\big\}$

## Dimostrazione

Il nostro obbiettivo è dimostrare che: $\mathcal{L}(DFA) \subseteq \mathcal{L}(NFA) \iff \mathcal{L}(NFA) \subseteq \mathcal{L}(DFA)$:

>[!note] Prima implicazione
>
>Dato $L \in \mathcal{L}(DFA)$, sia $D := (Q,\Sigma,\delta,q_{0},F)$ il DFA tale che $L= L(D)$
>
>Poiché il concetto di NFA è una generalizzazione del concetto di DFA, ne segue automaticamente che $D$ sia anche un NFA, implicando che $L \in \mathcal{L}(NFA)$ e di conseguenza che:
>
>$$
>\mathcal{L}(DFA) \subseteq \mathcal{L}(NFA)
>$$

>[!note] Seconda implicazione
>
>

