---
type: Uni Note
class:
  - "[[Automi (class)]]"
academic year: 2024/2025
related:
completed: false
created: 2025-09-26T08:36
updated: 2025-10-03T14:37
---
>[!note] Insieme dei Linguaggi Regolari
>
>Dato un alfabeto $\Sigma$, definiamo come insieme dei linguaggi regolari di $\Sigma$, indicato con REG, l’insieme delle classi dei linguaggi riconosciuti da un DFA:
>
>$$
>REG := \mathcal{L}(DFA) = \mathcal{L}(NFA)
>$$
>
>Dove:
>- La classe dei linguaggi di $\Sigma$ riconosciuti da un NFA il come: $\mathcal{L}(NFA) = \big\{\mathcal{L} \subseteq \Sigma^{*}\ |\ \exists\; \text{NFA}\ N \text{ t.c } \mathcal{L}= \mathcal{L}(N)\big\}$
>- La classe dei linguaggi di $\Sigma$ riconosciuti da un DFA il come: $\mathcal{L}(DFA) = \big\{\mathcal{L} \subseteq \Sigma^{*}\ |\ \exists\; \text{DFA}\ D \text{ t.c } \mathcal{L}= \mathcal{L}(D)\big\}$
>  
>>***Osservazione:*** $\mathcal{L}(DFA) = \mathcal{L}(NFA)$ grazie al teorema [[Equivalenza tra DFA e NFA|equivalenza tra DFA e NFA]]

## Chiusura dei linguaggi regolari

Obbiettivo dimostrare che se $L_{1},L_{2} \in REG$, allora:
- $L_{1} \cup L_{2} \in REG$
- $L_{1} \cap L_{2} \in REG$
- $\overline{L_{1}} = REG$
- $L_{1} \circ L_{2} \in REG$
  
>[!danger] Teorema: Chiusura dell'unione in REG
>
>>[!warning]- Dimostrazione
>>Induzione: $L_{1}, L_{2} \in REG \implies \exists M_{1}, M_{2} \in DFA\ \text{t.c.}\ L(M_{1}) = L_{1} \wedge L(m_{2}) = L_{2}$
>>
>>Dobbiamo definire $M 1 \text{t.c.}\ L(M) = L_{1} \cup L_{2}$ però abbiamo un *problema*, ovvero:
>> - dato `x` candidato non possono prima provare a vedere se $M(x)$ accettato.
>>   
>>*idea:* `M` deve eseguire $M_{1}$, $M_2$ in parallelo ...

>[!danger] Teorema: Chiusura dell’intersezione in REG
>
>>[!warning]- Dimostrazione

>[!danger] Teorema: Chiusura del complemento in REG
>
>>[!warning]- Dimostrazione

>[!danger] Teorema: Chiusura della concatenazione in REG
>
>>[!warning]- Dimostrazione

>[!danger] Corollario: Chiusura della potenza in REG
>

>[!danger] Teorema: Chiusura di star in REG
>
>>[!warning]- Dimostrazione

>[!danger] Corollario: Chiusura di pulus in REG
>
>