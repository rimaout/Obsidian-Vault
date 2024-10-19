---
type: Uni Note
class:
  - "[[Calcolo delle Probabilità (class)]]"
academic year: 2024/2025
related: 
completed: false
created: 2024-10-14T15:10
updated: 2024-10-19T19:22
---
>[!abstract] Index
>1. [[#Probabilità Condizionata]]
>	- [[#Proposizione 1]]
>	- [[#Proposizione 2 (regola del prodotto)]]
>2. [[#Teorema di Bayes]]
>3. [[#Formula Probabilità Totale]]
>4. [[#Probabilità Totale + Beyes]]

>[!abstract] Related
>-  [[Calcolo delle Probabilità (class)]]

>[!danger]- TLDR
>
>**Legge della Probabilità Totale:**
>
>$$
>P(E) = P(F) \cdot P(E \vert  F) + P(E^{c}) \cdot P(E \vert F^{c})
>$$
>
>**Teorema di Beyes:**
>
>$$
>P(F \vert E) = \frac{P(F) \cdot P(E \vert F) }{P(E)}
>$$
>
>**Probabilità Totale + Beyes:**
>
>$$
>P(F \vert E) = \frac{P(F) \cdot P(E \vert F) }{P(F)\cdot P(F) + P(E^{c})\cdot P(E \vert F^{c})}
>$$
>

---

## Probabilità Condizionata

Dati gli eventi $E$ ed $F$, con $P(F)>0$ si definisce la probabilità di $E$ condizionata a $F$ come:

$$
P(E \vert F) = \frac{P(E\cap F)}{P(F)}
$$

>[!example] Esempio
>Si sta lanciando un dado e prendiamo in considerazione questi eventi:
>- $E = \# \text{ Esce 1 o 2}$
>- $F = \# \text{ Esce un nemero}\leq 4$
>
>Normalmente la probabilità di $E$ è $P(E) = \frac{1}{3}$, ma se vogliamo calcolare la probabilità Di $E$ condizionata da $F$, allora otteniamo:
>
>$$
>P(E \vert F) = \frac{P(E\cap F)}{P(F)} = \frac{2}{4} = \frac{1}{2}
>$$

---
### Proposizione 1

Se $S$ è finito e ha esiti equi-probabili allora:
$$
P(E \vert F) = \frac{{ \lvert E \cap F \rvert }  }{{ \lvert F \rvert }  }
$$

Con $P(F)$ positiva

>[!warning]- Dimostrazione
>
>$$
> P(E \vert F) = \frac{P(E \cap F)}{P(F)} = \frac{ \frac{{ \lvert E \cap F \rvert }  }{{ \lvert S \rvert }  } }{ \frac{{ \lvert F \rvert }  }{{ \lvert S \rvert }  } } = \frac{E \cap  F}{F}
>$$

>[!example]- Esempio da rivedere 🟡
>Estraggo 3 carte da un mazzo da 40 senza rimpiazzo, sapendo che ho estratto solo carte di bastoni, qual è la probabilità di aver estratto un asso?
>- $E = \# \text{ Estraggo un asso}$
>- $E=\# \text{Estraggo solo bastoni}$
>- $S = \{ A \subset M: \lvert A \rvert = 3 \}$ dove $M$ è un mazzo di carte
>
>$$
>P(E \vert F) = \frac{{ \lvert E \cap F \rvert }  }{{ \lvert F \rvert }  } = \frac{\binom{9}{2}}{\binom{10}{3}} = \frac{3}{10}
>$$
>
>>**oss:** $\binom{9}{2}$ sono le terne non ordinate di bastoni dove non c'è l'asso

>[!example]- Esempio
>Ho un dado truccato dove 1 esce con probabilità $\frac{1}{2}$​ mentre gli altri numeri $\frac{1}{10}$​, qual è la probabilità che esca 1 o 2 sapendo che è uscito un numero $\leq 4$.
>
>- $E = \# \text{ Esce 1 o 2} = \{ 1,2 \}$
>- $F = \# \text{Esce un numero}\leq 4 = \{ 1,2,3,4 \}$
>- $S = \{ 1,2,3,4,5,6 \}$
>  
>Dove:
>- $E \cap F = \{ 1,2 \} \implies P(E \cap F) = P(\{ 1 \}) + P(\{ 2 \}) = \frac{1}{2} + \frac{1}{10} = \frac{3}{5}$
>- $P(F) = P(\{ 1,2,3,4 \}) = \frac{1}{2} + \frac{1}{10} \cdot 3 = \frac{4}{5}$ 
>  
>Quindi:
>$$
>P(E \vert F) = \frac{P(E\cap F)}{P(F)} = \frac{\frac{3}{5}}{\frac{4}{5}} = \frac{3}{4}
>$$

---
### Proposizione 2 (regola del prodotto)

>[!note] Formula Generale
>
>Siano $E_{1}, \dots, E_{n}$ eventi, allora:
>
>$$
>\begin{align*}
>& P(E_{1} \cap \dots \cap  E_{n}) = P(E_{1}) \cdot  P(E_{2}\vert E_{3}) \cdot  P(E_{3} \vert E_{1} \cap E_{2}) \cdot  \dots \cdot  P(E_{n}\vert E_{1} \cap \dots \cap E_{n-1}) \\
>\end{align*}
>$$
>
>Supponendo che $P(E_{1} >0, \ \ P(E_{1}\cap E_{2})>0, \dots ,P(E_{1} \cap \dots \cap E_{n-1}) > 0)$

>[!warning] Casi Comuni
>
>$$
>\begin{align*}
>& n=2 \ \ \to  \ \ P(E_{1} \cap E_{2}) = P(E_{2}) \cdot  P(E_{1} \vert E_{2})\\
>& n=3 \ \ \to  \ \ P(E_{1} \cap  E_{2} \cap  E_{3}) = P(E_{1}) \cdot P(E_{2}\vert E_{1}) \cdot  P(E_{3}\vert E_{1} \cap  E_{2})
>\end{align*}
>$$

>[!example] Esempio
>Estraggo 3 carte senza rimpiazzo da un mazzo da 40, qual è la probabilità che la prima carta è di bastoni, la seconda di denari e la terza di bastoni.
>
>$G = \# \text{ 1° carta bastoni, 2° carta denari, 3° carta bastoni}$
>
>Calcolare $P(G)$
>
>$G = E_{1}  \cap E_{2} \cap E_{3}$
>
>Dove:
>- $E_{1} = 1° \text{carta è Bastoni}$
>- $E_{2} = 2° \text{carta è Denara}$
>- $E_{3} = 3° \text{carta è Bastoni}$
>  
>  Per regola del prodotto:
>  $$
>P(G) = P(E_{1} \cap  E_{2} \cap  E_{3}) = P(E_{1}) \cdot  P(E_{2}\vert E_{1}) \cdot  P(E_{3}\vert E_{1} \cap  E_{2}) = \frac{10}{40} \cdot  \frac{10}{39} \cdot  \frac{9}{38}
>$$

---
## Teorema di Bayes

Tra due eventi $A$ e $B$

$$
P(A \vert B) := \frac{P(A \cap  B)}{B} = \boxed{\frac{P(A) \cdot  P(B\vert A)}{P(B)}}
$$

>[!note] Formula Generalizzata
>
>$$
>P(F_{i} \vert E) = \frac{P(F^{i})\cdot P(E\vert F_{i})}{\sum\limits^{n}_{j = i} P(F_{j}) \cdot P(E \vert F_{j})}
>$$

>[!example]- Esempio Formula Generalizzata (aerei)
>Un aereo è scomparso e si presumere che possa essere con uguale probabilità in tre possibili zone ($Z_{1},Z_{2},Z_{3}$)
>
>Indichiamo con:
>- $\beta_{i}$ la probabilità di NON trovare l'aereo in $Z_{i}$, se è realmente in $Z_{i}$
>- $1- \beta_{i}$ la probabilità di trovare l'aereo in $Z_{1}$, se è effettivamente in $Z_{i}$
>- $R_{i} = \#\text{l'aereo è in }Z_{i}$
>- $E = \text{la ricerca in } Z_{1} \text{ha dato esito negativo}$
>
>Calcolare la probabilità che l'aereo sia in $Z_{1}$, sapendo che la ricerca in $Z_{1}$ ha dato esito negativo: 
>>**oss:** $P(R_{1}) = P(R_{2}) = P(R_{3}) = \frac{1}{3}$
>  
>$$
>P(R_{1}\vert E) = \frac{P(E \cap  R_{1})}{P(E)} = \frac{P(R_{1})\cdot  P(E \vert R_{1})}{P(E)} = \frac{P(R_{1})\cdot P(E \vert R_{1})}{\sum\limits^{3}_{k=1}P(R_{k})\cdot P(E\vert R_{k})} = \frac{\frac{1}{3} \cdot \beta_{1}}{\frac{1}{3}\beta_{1}+ \frac{1}{3}\cdot 1+ \frac{1}{3} \cdot  1} = \frac{\beta_{1}}{\beta_{1}+2}
>$$
>
>Adesso calcoliamo la probabilità che l'aereo sia in $Z_{1}$ o in $Z_{2}$, prendendo $j =1,2$
>
>$$
>P(R_{j} \vert E) = \frac{P(R_{j})\cdot P(E\vert R_{j})}{P(E)} = \frac{\frac{1}{3} \cdot  1}{\frac{1}{3}\beta_{1} + \frac{1}{3} + \frac{1}{3}} = \frac{1}{\beta_{1}+1}
>$$
>
>>**oss:** La formula mostra che la probabilità condizionale è $\frac{1}{\beta_{1}+1}$​, che dipende dalla probabilità di non trovare l'aereo in $Z_{1}$​ se è effettivamente in $Z_{1}$​ (rappresentata da $\beta_{1}$​).

---
## Formula Probabilità Totale

Dati $E, F$ eventi, allora:

$$
P(E) = P(F) \cdot  P(E\vert F) \cdot  P(F^{c}) \cdot  P(E\vert F^{c})
$$

>[!warning]- Dimostrazione
>$E = (E \cap F) \cup (E \cap F^{c})$
>
>Quindi dato che sono incompatibili:
>$$
>P(E) = P(E\cap F) + P(E\cap  F^{c}) \overset{\text{regola del prodotto}}{=} P(F) \cdot  P(E \vert F) + P(F^{c}) \cdot  P(E\vert F^{c})
>$$

>[!note] Formula Generalizzata
>Siano $F_{1}, \dots, F_{n}$ eventi 2 a 2 disgiunti (cioè incompatibili) tali che $S = \bigcup\limits^{n}_{i=1}f_{i}$ 
>
>Allora per ogni $E$ vale:
>
>$$
>P(E) = \sum^{n}_{i=1} P(F_{i}) \cdot P(E \vert F_{i})
>$$

---
## Probabilità Totale + Bayes

$$
P(F \vert E) = \frac{P(F) \cdot P(E \vert  F) }{P(F)\cdot P(F) + P(E^{c})\cdot P(E \vert  F^{c})}
$$
---
## Proposizione 3


Sia $F$ evento con $P(F)>0$, Allora la funzione $R \to P(F \vert F)$ , al variare di $E$ eventi, è una funzione di probabilità

>[!warning] Conseguenze
>
>- $P(E^{c}\vert F) = 1- P(E\vert F)$
>- $P(A\cup B \vert F) = P(A\vert F) + P(B\vert F) - P(A\cap B\vert F)$
>- $A_{1}, \dots, A_{n}$ eventi 2 a 2 disgiunti allora: 
>$$
>P\left( \bigcup^{n}_{i=1} \right) = \sum^{n}_{i=1}P(A_{i}\vert F)
>$$

---