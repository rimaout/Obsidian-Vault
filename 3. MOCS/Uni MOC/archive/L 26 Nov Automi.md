---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2025-11-26T08:25
updated: 2025-11-26T10:09
---
## Classe P

- Il tempo limita lo spazio
- Nella teoria avere una macchina con 1 nastro o averne una con più nastri non cambia il costo asintotico
- Nella pratica però cambia, ad esempio:
  
  Ad esempio un macchina che riconosce stringhe palindrome, se è a singolo nastro richiede $O(n^{2})$ se a due nastri richiede $O(n)$.

**Teorema:** (non lo dimostriamo)
- Ogni TM a singolo nastro necessità $\Omega(n^{2})$ tempo per determinare se una stringa è palindroma

**Definizione:** classe DTIME (vedi appunti)

`P` è la classe di linguaggi decidibili da TM in tempo polinomiale, nella lunghezza dell'input, ovvero:
$$
P = \bigcup_{k \in \mathbb{N}} \text{DTIME}\, (n^{k})
$$
Questa definizione è robusta perché è in variante rispetto al modello di TM.

**Definizione:** classe `EXP`, ovvero la classe di linguaggi decidibili in tempo esponenziale.

$$
\text{EXP} = \bigcup_{k \in \mathbb{N}} \text{DTIME}\, \Big(2^{n^{k}}\Big)
$$

oss: teorema di gerarchia di tempo, ovvero un linguaggio polinomiale può essere anche risolto in un tempo esponenziale.

Quindi l'insieme `P` è un sotto insieme di `EXP`.

La classe `EXP` è un insieme molto grande, ci sono linguaggio che sono sono exp, che utilizzando utilizzando strategie intelligenti, possono essere portati in `P`.

## Satisfability (soddisfacibilità)

**Def** un corcuito boleano è un grafo diretto aciclico, con `n` input $x_{1}, \dots,x_{n}$ e un output.

ldjlkasjlkfjl porte: $\wedge \vee not$

disegnino

Se `fan-out = 1`, $C$ è una formula.
- dove `fan-out` è il numero di cavi in uscita da una porta

**Def** $Circuit-Eval = \{ <C,x>:\ C(x)=1 \}$

Dove C è un circuito, ...

$\mid<C>\mid = O(n\log n)$

**def** $Ciruit-Sat = \{ <C>: \exists x \in \{ 0,1 \}^{n} \text{ t.c. } C(x)=1  \}$

Ovviamente circuit-sat appartiene a EXP, perchè ...

- Formula sat: C è una formula
- CNF-SAT: C è una CNF cioè un  ...
- K-SAT: tutte le clausole hanno k letterali

Esempio: `3-SAT` ovvero $k=3$

...

I migliori algoritmi per:
- 3SAT appartengono a $DTIME(1,34^{n})$
- 4SAT appartengono a $DTIME(1,5^{n})$

**Teo:** 2SAT appartiene a `P`

