---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2026-09-29T17:08
updated: 2026-10-01T13:44
---
Dato il linguaggio $L = \{11, 110\}^{*}$, costruire un NFA N con 4 stati che riconosca L. Convertire il NFA in un DFA M equivalente.

$N = (Q_{N}, \delta_{N}, \Sigma, q_{0}, F_{N})$ dove:
- $Q_{N} = \{ q_{0},q_{1},q_{2} \}$
- $F = \{ q_{0} \}$

$N = (Q_{D},\delta_{D}, \Sigma, q_{0}, F_{D})$ dove:
- $Q_{N} = {\cal P}(Q_{N})$
- $F_{D} = \{ R \in Q_{N} : R \cap F_{N} \not = \emptyset\}$

$$
\delta(R,a)_{D} = \bigcup_{q\in R} E\big(\delta(q,a)_{N}\big)
$$

$$
E(R) = \{ q \in Q_{N} : \text{è possibile raggiungere q in N utilizando soltanto } \epsilon \text{ archi}\}
$$

### Problema 1.4

**Dimostrazione.** Sia $L = \{w \in \{0,1\}^{*} : |w|_{0} = |w|_{1}\}$. Dimostriamo che $L \in REG$.

**Pumping lemma.** Se $L$ è regolare, allora esiste $p > 0$ tale che, per ogni $w \in L$ con $|w| \geq p$, esiste una suddivisione $w = xyz$ tale che:
- $|xy| \leq p$
- $|y| > 0$
- per ogni $i \geq 0, xy^{i}z \in L$

**Procediamo per assurdo.** Supponiamo che $L$ sia regolare. Allora, per il pumping lemma, esiste una lunghezza di pumping $p > 0$.

Consideriamo la stringa $w = 0^{p}1^{p}$. Si ha che:
- $w \in L$, perché contiene $p$ zeri e $p$ uni;
- $|w| = 2p \geq p$.

Per il pumping lemma esiste quindi una suddivisione $w = xyz$ con $|xy| \leq p$ e $|y| > 0$.

Poiché $|xy| \leq p$, i simboli di $xy$ si trovano tutti nel blocco iniziale di $p$ zeri di $w$.

Consideriamo ora i = 2. La stringa xy²z, questa stringa avra un numero maggiore di zeri rispoetto a numero di uni, in quanto abbiamo aumentato solo y (che contiene solo 0) e il numero di seri è rimasto invariato rispetto a $xy^{2}z$. Quindi $xy^{2}z \not \in L$ e 1uesto contraddice la tesi del pumping lemma, secondo cui xyⁱz ∈ L per ogni i ≥ 0.

Concludiamo che L ∉ REG. 

## Problema 1.5 

**Dimostrazione.** Dato il linguaggio $L = \{ 1^{n^{2}} | n \in N \}$, dimostrare che $L \not \in REG$

**Pumping lemma.** Se $L$ è regolare allora esiste $p>0$ tale che, per ogni $w \in L$ con $|w| \geq p$ esiste una suddivisione $w := xyz$ tale che:
- $|xy|\leq p$
- $|y|>0$
- $\forall i \in \mathbb{N}\ \ xy^{i}z \in L$ 
  
**Procediamo per Assurdo.** Sia per assurdo $L \in REG$, allora per il pumping lemma esiste una lunghezza di pumping $p > 0$.

Consideriamo ora la stringa $w = 1^{p^{2}}$ si ha che:
- $w \in L$
- $|w| = p^{2} > p$


