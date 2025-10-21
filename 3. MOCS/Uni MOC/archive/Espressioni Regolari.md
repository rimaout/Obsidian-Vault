---
type: Uni Note
class:
  - "[[Automi (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-10-03T14:40
updated: 2025-10-10T12:10
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
>
>Dato un alfabeto $\Sigma$, definiamo come espressione regolare di $\Sigma$ una stringa $R$ rappresentante un linguaggio $L(R) \subseteq \Sigma^{*}$. In altre parole, ogni espressione regolare $R$ rappresenta in realtà il linguaggio $L(R)$ ad essa associata.
>
>In particolare definiamo, ricorsivamente, l’insieme delle espressioni regolari di $\Sigma$, indicato con $re(\Sigma)$, come:
>
>$$
>\text{Caso Base: } \begin{cases}
>\ \emptyset &\in re(\Sigma) \\
>\ \epsilon &\in re(\Sigma) \\
>\ a &\in re(\Sigma),\ \text{dove } a \in \Sigma
>\end{cases}
>$$
>
>$$
>\text{Caso Induttivo:} \begin{cases}
>\ R_{1} \cup R_{2} &\text{se } R_{1},R_{2} \in re(\Sigma) \\
>\ R_{1} \circ R_{2} &\text{se } R_{1},R_{2} \in re(\Sigma) \\
>\ (R_{1})^{*} &\text{se } R_{1} \in re(\Sigma)
>\end{cases}
>$$

>[!note] Linguaggio di un espressione regolare
>Sia $\Sigma$ un alfabeto
>
>Ogni espressione regolare ha associato un linguaggio $L(r)\ \text{ t.c }\ r \in re(\Sigma)$:
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

## Linguaggio ottenuto da espressione regolare può essere ottenuto da NFA

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
>**Caso Base:**
>
>>Se $R = \emptyset$ allora $L(R) = \emptyset$, e il seguente NFA riconosce $L(R)$:
>>
>>![[Pasted image 20251009173333.png|250]]
>>
>>***Formalmente:*** $N = \big( \{ q_{0} \},\Sigma,\delta,q_{0}, \emptyset \big)$ dove $\delta(r,b)=\emptyset$ per ogni $r$ e $b$.
>
>>Se $R = \epsilon$ allora $L(R) = \{ \epsilon \}$, e il seguente NFA riconosce $L(R)$:
>>
>>![[Pasted image 20251009175812.png|250]]
>>
>>***Formalmente:*** $N = \big( \{ q_{0} \},\Sigma,\delta,q_{0}, \{ q_{0} \} \big)$ dove $\delta(r,b)=\emptyset$ per ogni $r$ e $b$.
>
>>Se $R = a$ per qualche $a \in \Sigma$, allora $L(R) = \{ a \}$, e il seguente NFA riconosce $L(R)$:
>>
>>![[Pasted image 20251009180256.png|400]]
>>
>>***Formalmente:*** $N = \big( \{ q_{0},q_{1} \},\Sigma,\delta,q_{0}, \{ q_{1} \} \big)$ dove $\delta(q_{1},a)=q_{2}$ e $\delta(r,b) = \emptyset$ per ogni $r\not=q_{1}$ e $b\not=a$.
>
>---
>
>**Ipotesi Induttiva:**
>
>Date $R_{1}, R_{2} \in re(\Sigma)$, assumiamo che 
>
>$$\exists \text{ NFA }N1, N2 \mid L(R_{1}) = L(N_{1}),\ L(R_{2}) = L(N_{2})$$ 
>
>dunque che $L(R_{1}), L(R_{2}) \in L(\text{NFA})$
>
>---
>
>**Passo Induttivo:**
>
>>Se $R = R_{1} \cup R_{2}$, tramite la Chiusura dell’unione in REG, otteniamo che:
>>$$
>>L(R) = L(R_{1}) \cup L(R_{2}) = L(N_{1}) \cup  L(N_{2}) \in REG = L(\text{NFA})
>>$$
>
>>Se $R = R_{1} \circ R_{2}$, tramite la Chiusura della concatenazione in REG, otteniamo che:
>>$$
>>L(R) = L(R_{1}) \circ L(R_{2}) = L(N_{1}) \circ L(N_{2}) \in REG = L(\text{NFA})
>>$$
>
>>Se $R = (R_{1})^{*}$, tramite la Chiusura di plus in REG, otteniamo che:
>>$$
>>L(R) = L(R_{1})^{*} = L(N_{1})^{*} \in REG = L(\text{NFA})
>>$$

## Conversione da espressione regolare a NFA

>[!note] Regole Base
>
>![[Pasted image 20251010115745.png|800]]

>[!example] Esempio
>
>Consideriamo l'espressione regolare $(a \cup ab)^{*}$, costruiamo il NFA corrispondente a tale espressione partendo dai suoi sotto-componenti:
>
>![[Pasted image 20251010120840.png|950]]
