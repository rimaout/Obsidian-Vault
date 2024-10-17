---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2024-10-14T16:30
updated: 2024-10-14T18:30
---
>[!abstract] Index
>1. 

>[!abstract] Related
>- 

>[!danger] TLDR

---

## Correzione esercizi per casa

>[!example] Es 1

>[!example] Es 2
>- $E =\# \text{lo studente traduce bene}$
>- $F = \# \text{lo studente ha il cerificato cambrige}$
>
>dove: 
>- $P(F) = 0.60$  
>- $P(E \mid F) = 0.90$
>- $P(E\mid F^{c}) = 0.60$
>
>$$
>P(F^{c} \mid E) = \frac{P(E \cap  F^{c})}{ P(E)} = \frac{ P(F^{c}) \cdot P(E \mid F^{c})}{P(F^{c}) \cdot P(E\mid F^{c}) + P(F) \cdot P(E \mid F) } = \frac{0.4 \cdot  0.6}{0.4 \cdot  0.6 +  0.6 \cdot 0.9} = \frac{4}{13}
>$$

>[!example] Es 3
>In una comunità il %36 percento delle famiglie ha un cane .....
>
>- $C = \# \text{la familgia ha il cane}$
>- $G = \# \text{la faliglia ha il cane}$
>  
>  Dove:
>  - $P(C) = 0.36$
>  - $P(G) = 0.30$
>  - $P(G \vert C) = 0.22$
>    
>  **Domanda a):** Qual'è la probabilità che una famiglia abbia sia un cane che un gatto ?
>
>$$
>P(C \cap  G) = P(C)\cdot  P(G \vert C) = 0.36 \cdot  0.22 = 0.0792
>$$
>
>  **Domanda b):** Qual'è la probabilità che una famigli che possiede un cane prenda anche un gatto
>  
>$$
>P(C \mid G) = \frac{P(C \cap G)}{P(G)} = \frac{0.0792}{0.3} = 0.264
>$$

>[!example] Es 4
>Si considera due scatole una contenente un ...
>
>- $S_{1} = \{ n,b \}$
>- $S_{2} = \{ n,n,b \}$
>
>- $E = \# \text{ il sasso è nero}$
>- $F =\# \text{la scatola è }S_{1}$
>
>>**oss:** $P(F) = \frac{1}{2}$
>
>Calcolare P(E):
>
>$$
>P(E) = P(F) \cdot  P(E \vert F) + P(F^{c}) \cdot  P(E \vert F^{c}) = ffsvdsvszvfds
>$$
>
>$$
>P(F\vert E^{c}) = \frac{P)F \cap  E^{c}}{P(E^{c})} = \frac{P(F) \cdot P(E^{c} \vert F)}{P(E^{c})} = \frac{\frac{1}{2} \cdot  \frac{1}{2}}{\frac{5}{12}} = \frac{1}{4} \cdot \frac{12}{5} = \frac{3}{5}
>$$

>[!example] Es 32
>100 famiglie ....

>[!example] Es 35
>Il regalo di compleanno è stato nascosto
>- $M = \# \text{ la mamma ha nascosto il regale}$
>- $M^{c} = \# \text{il papà ha nascosto il regalo}$
>
>Dove:
>- $P(M) = 0.6$
>- $P(M^{c}) = 0.4$
>
>La posizione del regalo:
>- $U = \# \text{ il regalo è ala piano di sopra (up)}$ 
>
>Dove:
>- $P(U \vert M) = 0.7$ 
>- $P(U\vert M^{c}) = 0.5$
>  
>  Per calcolare $P(U)$ dobbiamo usare la legge della probabilità totale
>  
>$$
>P(U) = P(M) \cdot  P(U\vert M) + P(M^{c}) \cdot  P(U \vert M^{c}) = 0.6 \cdot  0.7 + 0.4 \cdot  0.5 = 0.62
>$$
>
>Sapenso che il regalo è nascosto al piano di sopra quanto è probabile che lo abbia nascosto il papà? (Usiamo bayes)
>
>$$
>P(M^{c} \vert U^{c}) = \frac{P(M^{c} \cap  U^{c})}{P(U^{c})} = \frac{P(M^{c}) \cdot  P(U^{c} \vert M^{c})}{P(U^{c})} = \frac{0.4 \cdot  0.5}{0.38}
>$$

>[!example] Es 36
>Tre negozi A, B, C
>
>Dove:
>

| Negozio:                | A   | B   | C   |
| ----------------------- | --- | --- | --- |
| Numero Dipendenti       | 50  | 75  | 100 |
| % Dipendenti Donna      | %50 | 60% | 70% |
| Numero Dipendenti Donna | 25  | 45  | 70  |

---
## Prop. Legge della probabilità totale generalizzata

Siano $F_{1}, f_{3}, \dots , F_{n}$ evento 2 a 2 distinti (cioè incompatibili) tali che $S = \bigcup^{n}_{i=1}F_{i}$

Allora per ogni evento E vale che:
$$
P(E) = \sum^{n}_{i=1}P(F_{i})P(E \vert F_{i})
$$
es: n = 2

$$
P(E) = P(F_{1})P(E \vert F_{1}) + P(F_{2}) P(E \vert F_{2})
$$
>[!warning] Dimostrazione
>
>$$
>E = (E \cap  F_{1}) \cup (E \cap F_{2}) \cup \dots \cup (E\cap F(n))
>$$
>
>Quindi
>
>$$
>P(E) = P(E \cap F_{1}) + P(E\cap F_{2}) + \dots + P(E\cap F_{n}) ojjdkhvlkjsdbdlkjlsjk
>$$