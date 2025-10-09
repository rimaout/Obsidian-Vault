---
type: Uni Note
class:
  - "[[Automi (class)]]"
academic year: 2024/2025
related:
completed: false
created: 2025-10-03T14:40
updated: 2025-10-09T17:33
---
## Introduzione

In aritmetica, possiamo usare le operazioni `+` e `x` per costruire espressioni come

$$(5+3) \times 4.$$

Analogamente, possiamo usare le operazioni regolari per costruire espressioni che descrivono linguaggi, che sono chiamate espressioni regolari, ad esempio:

$$(O \cup 1)\cdot 0^{*}$$

Il valore dell'espressione aritmetica è il numero 32. Il valore di un'espressione regolare è un linguaggio. In questo caso, il valore è il linguaggio che consiste di tutte le stringhe che iniziano con uno `0` o un `1` seguito da un qualsiasi numero di simboli uguali a `0`.

## Definizione Espressione Regolare

$R$ è un espressione regolare (una stringa) che descrivere delle regole per riconoscere un linguaggio $L(R)$.

$L(R)$ è il linguaggio riconosciuto dall’espressione regolare $R$ (come vedremo è possibile creare un automa che riconosce $L(R)$).

>[!note] Definizione Formale
>Sia $\Sigma$ un alfabeto
>
>Ogni espressione regolare ha associato un linguaggio $L(r)$ t.c $r \in re(\Sigma)$:
>
>$$
>\text{Caso Base: } \begin{cases}
>L(r) = \emptyset &r = \emptyset \\
>L(r) = \{ \epsilon\} &r = \epsilon \\
>L(r) = \{ a \} &r = a
>\end{cases}
>$$
>
>$$
>\text{Caso Induttivo:} \begin{cases}
>L(r) = L(R_{1}) \cup L(R_{2}) &\text{se } r = R_{1} \cup  R_{2} \\
>L(r) = L(R_{1}) \circ L(R_{2}) &\text{se } r = R_{1} \circ  R_{2} \\
>L(r) = \big( (R_{1}) \big)^{*} &\text{se } r = R_{1}^{*}
>\end{cases}
>$$

^158ca6

>[!example]- Esempi
>
>- $\Sigma^{*}1$ tutte le stringhe che finiscono con 1
>- $0^{*}1$ tutte le stringhe composte da un numero indefinito di zeri e che terminano con 1
>- $0^{+}1$ tutte le stringhe composte da un numero indefinito di zeri (ma almeno uno) e che terminano con 1
>
>L'espressione che rappresenta tutte le stringhe composte dai caratteri `0` e `1`
>$$
>\textcolor{orange}{0^{*}1} = 0^{*} \circ 1 = \{ 0 \}^{*} \circ \{ 1 \} = \{ \epsilon, 0, 00, \dots \} \circ \{ 1 \} = \{ \epsilon \circ 1, 0\circ 1, 00 \circ 1, \dots \} = \{ 1, 01, 001, 0001, \dots \}
>$$
>
>$\Sigma^{+}1\Sigma^{*} = \Sigma^{+} \circ 1 \circ \Sigma^{*}$ 
>
>Dove:
>- $\{ 0 \}$ è il linguaggio che contiene soltanto la stringa composta da `0`
>- $\{ 0 \}^{*} = \{ 0 \}^{0} \cup \{ 0 \}^{1} \cup \{ 0 \}^{2} \cup \dots\ = \{ \epsilon,0, 00, 000, 0000, \dots \}$  
>- $\{ 0 \}^{+} = \{ 0 \}^{1} \cup \{ 0 \}^{2} \cup \{ 0 \}^{3} \cup \dots\ = \{ 0, 00, 000, 0000, \dots \}$ 
>- $\{ 0, 00 \} \circ \{ 1, 12 \}$ = $\{ 0 \circ 1, 0 \circ 12, 00 \circ 1, 00 \circ 12\}$ = $\{ 01,012,001,0012 \}$
>
>$$(1^{2} \cup 2) = \{ 11 \} \cup 2 = \{ 11,2 \}$$
>
>$$
>\Sigma = \{ 0,1 \}
>$$
>$$
>\begin{align*}
>& 0^{*}1^{+}0^{*}\\
>& \Sigma^{*}001\Sigma^{*}\\
>&1^{*}(01^{+})^{*}
>\end{align*}
>$$

## Classe dei linguaggi descritti da esp. reg

Se un linguaggio è descritto da un espressione regolare, allora esso è regolare

>[!note] Definizione classe dei linguaggi descritti da esp. reg
>
>Dato un alfabeto $\Sigma$, definiamo come classe dei linguaggi di $\Sigma$ descritti da un’espressione regolare il seguente insieme:
>
>$$
>\mathcal{L(re)} = \{ L \subseteq \Sigma^{*} \mid \exists R \in \mathrm{Re}(\Sigma) \text{ t.c } L = L(R)  \}
>$$

## Conversione da espressione regolare a NFA

>[!note] Lemma
>
>Date le due classi dei linguaggi $\mathcal{L}(re)$ e $\mathcal{L}(NFA)$, si ha che
>
>$$
>\mathcal{L}(re) \subseteq \mathcal{L}(NFA)
>$$

>[!warning] Dimostrazione
>
>Procediamo per induzione strutturale, ossia dimostrando che per ogni sotto-componente vale una determinata proprietà allora essa varrà anche per ogni componente formato da tali sotto-componenti.
>
>In particolare dimostreremo che ognuna delle 6 componenti base della [[#^158ca6|definizione di espressione regolare]] dimostreremo può essere conferita in un NFA.
>
>---
>
>**Casi Base:**
>
>>Se $R = \emptyset \in re(\Sigma)$ allora $L(R) = \emptyset$, e il seguente NFA riconosce $L(R)$:
>>
>>![[Pasted image 20251009173333.png|250]]
>
>
>
>---
>
>**Passo Induttivo:**
>

