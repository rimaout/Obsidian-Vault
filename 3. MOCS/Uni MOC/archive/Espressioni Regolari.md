---
type: Uni Note
class:
  - "[[Automi (class)]]"
academic year: 2024/2025
related:
completed: false
created: 2025-10-03T14:40
updated: 2025-10-03T17:12
---
## Definizione

$R$ è un espressione regolare (una stringa) che descrivere delle regole per riconoscere un linguaggio $L(R)$.

$L(R)$ è il linguaggio riconosciuto dall’espressione regolare $R$ (come vedremo è possibile creare un automa che riconosce $L(R)$).


Sia $\Sigma$ un alfabeto

Un espressione regolare su $\Sigma$, rappresentata con $re(\Sigma)$ è definita ricorsivamente:

$$
\text{Caso Base: } \begin{cases}
\emptyset &\in re(\Sigma)\\
\epsilon &\in re(\Sigma) \\
a &\in re(\Sigma),\ a \in \Sigma
\end{cases}
$$
$$
\text{Caso Induttivo:} \begin{cases}
R_{1} \cup R_{2} & R_{1},R_{2}\in re(\Sigma) \\
R_{1} \circ R_{2} & R_{1},R_{2}\in re(\Sigma) \\
(R_{1})^{*} & R_{1}\in re(\Sigma)
\end{cases}
$$


Ogni espressione regolare ha associato un linguaggio $L(r)$ t.c $r \in re(\Sigma)$:

$$
\text{Caso Base: } \begin{cases}
L(r) = \emptyset &r = \emptyset \\
L(r) = \{ \epsilon\} &r = \epsilon \\
L(r) = \{ a \} &r = a
\end{cases}
$$
$$
\text{Caso Induttivo:} \begin{cases}
L(r) = L(R_{1}) \cup L(R_{2}) &\text{se } r = R_{1} \cup  R_{2} \\
L(r) = L(R_{1}) \circ L(R_{2}) &\text{se } r = R_{1} \circ  R_{2} \\
L(r) = \big( (R_{1}) \big)^{*} &\text{se } r = R_{1}^{*}
\end{cases}
$$

- $\Sigma^{*}1$ tutte le stringhe che finiscono con 1
- $0^{*}1$ tutte le stringhe composte da un numero indefinito di zeri e che terminano con 1
- $0^{+}1$ tutte le stringhe composte da un numero indefinito di zeri (ma almeno uno) e che terminano con 1



Un espressione regolare R è un operazione su ... che da come output un linguaggio L(R) riconosciuto dall’espressione regolare R.


(5 * 2) + (7 * 3)



L'espressione che rappresenta tutte le stringhe composte dai caratteri `0` e `1`
$$
\textcolor{orange}{0^{*}1} = 0^{*} \circ 1 = \{ 0 \}^{*} \circ \{ 1 \} = \{ \epsilon, 0, 00, \dots \} \circ \{ 1 \} = \{ \epsilon \circ 1, 0\circ 1, 00 \circ 1, \dots \} = \{ 1, 01, 001, 0001, \dots \}
$$
$\Sigma^{+}1\Sigma^{*} = \Sigma^{+} \circ 1 \circ \Sigma^{*}$ 

Dove:
- $\{ 0 \}$ è il linguaggio che contiene soltanto la stringa composta da `0`
- $\{ 0 \}^{*} = \{ 0 \}^{0} \cup \{ 0 \}^{1} \cup \{ 0 \}^{2} \cup \dots\ = \{ \epsilon,0, 00, 000, 0000, \dots \}$  
- $\{ 0 \}^{+} = \{ 0 \}^{1} \cup \{ 0 \}^{2} \cup \{ 0 \}^{3} \cup \dots\ = \{ 0, 00, 000, 0000, \dots \}$ 
- $\{ 0, 00 \} \circ \{ 1, 12 \}$ = $\{ 0 \circ 1, 0 \circ 12, 00 \circ 1, 00 \circ 12\}$ = $\{ 01,012,001,0012 \}$


$$(1^{2} \cup 2) = \{ 11 \} \cup 2 = \{ 11,2 \}$$



$$
\Sigma = \{ 0,1 \}
$$

$$
\begin{align*}
& 0^{*}1^{+}0^{*}\\
& \Sigma^{*}001\Sigma^{*}\\
&1^{*}(01^{+})^{*}
\end{align*}
$$
