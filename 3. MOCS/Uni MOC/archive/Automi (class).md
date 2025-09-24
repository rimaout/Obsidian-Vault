---
type: "[[Uni MOC]]"
academic year: 2024/2025
created: 2025-09-24T08:15
updated: 2025-09-24T11:19
---
Professore: [Daniele Venturi](https://corsidilaurea.uniroma1.it/it/users/danieleventuriuniroma1it)

Domande del corso: Quali sone le limitazioni intrinseche della computazione

**Argomenti:**
- *Teoria degli automi*, in particolare vedremo gli automi a stati finiti che sono il primo passo per capire modelli semplici di computazione.
- *Commutabilità*, consiste nello studio di quello che si può e non può fare con i computer. Dover per computer intendiamo il modello della macchina di Turing (modello semplificato di un computer). Vedremo che esistono problemi che nessun computer può risolvere. Esempio "stabilire se un programma (macchina di touring) termina" non può essere risolto da un computer, indipendentemente dalla risorse (alt problem).
- *Complessità*, quantificheremo le risorse necessarie (spazio e tempo) per risolvere un problema.

## Linguaggi Regolari

Il primo modello che vediamo è l'**automa a stati finiti** (DFA) deterministico. Molte semplice dato che processa l'input in modo sequenziale (bit a bit, carattere a carattere, ecc.

Ogni automa ha:
- uno stato iniziale (`q1`)
- uno stato di accettazione
- delle transizioni

>[!note] Definizione
>
>Un DFA è una tupla $Q,\ \Sigma,\ \delta,\ q_{0},\ f$, dove:
> - $Q$ è l'insieme finite degli stati
> - $\Sigma$
> - $\delta$ è una funzione  che prende in input $Q$ e $\Sigma$ quindi $\delta := Q \times \Sigma \to Q$
> - $q_{0}$ è lo stato iniziale
> - $f$ è l'insieme stati finali


Esempio:



Se `M` è un DFA, l’insieme delle stringhe riconosciute da `M` è detto `L(M)`, ovvero il linguaggio dell'automa è l’insieme di stringhe riconosciute.


Per definire precisamente il linguaggio introduciamo la funzione di transizione estesa: $\delta^{*}:\ Q \times \Sigma^{*} \to Q$

$$
\begin{cases}
&\delta^{*}(q, \epsilon) = \delta(q, \epsilon)\\ \\
&\delta^{*}(q, ax) = \delta^{*}(\delta(q,a), x)\ \text{ dove }\ x \in \Sigma^{*}. a \in \Sigma
\end{cases} \\
$$

Una **configurazione** è una coppia in  $Q \times \Sigma^{*}$

Dato $x \in \Sigma^{*}$, la *configurazione universale* 

**Passo di computazione**: parto da una configurazione ad un'altra rispettando $\delta$.

**Relazione binaria:**
$$(p, ax) |-_{M} (q,x) \iff \delta(p, e) = q$$
Dove:
- $p, q \in Q$ 
- $a \in \Sigma$
- $x \in \Sigma^{*}$

La possiamo estendere dlsfhkjsfdhakjfdh la *chiusura riflessiva* e *transitiva* :
$$
\begin{align*}
&(i)\ \ \ \ \ (q,x) |-_{M}^{*} (q, x)\\
&(i_{n}) \ \ \  (q,aby) |-_{M}^{*} (p,by)\ \ \wedge \ \ (q,by)|-_{M}(r,y sdfhkhfd)
\end{align*}
$$

>[!note] Linguaggio Accettatto
>
>Diciamo che $x \in \Sigma^{*}$ è accettato da $M = (Q, \Sigma, \delta, q_{0}, f)$ se $\sigma^{*}(q_{0}, x) \in f$ oppure $(q_{0,x}) |-_{M}^{*} (q,\epsilon)$ dove $q \in f$.
>
>In altre parole:
>$$
>L(M) = \{x \in \Sigma^{*}: \Sigma^{*}(q_{0},x)\in f\}
>$$


