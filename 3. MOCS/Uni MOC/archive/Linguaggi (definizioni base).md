---
type: Uni Note
class:
  - "[[Automi (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-09-25T16:47
updated: 2026-01-31T13:32
---
>[!note] Definizione 1: Alfabeto 🟢
>
>Definiamo come *alfabeto* un insieme finito di elementi detti *simboli*.
>
>***Esempio:***
>- L’insieme $\Sigma = \{0, 1, x, y, z\}$ è un alfabeto
>- L’insieme $\Sigma = \{0, 1\}$ è un alfabeto detto *binario*

>[!note] Definizione 2: Stringa 🟢
>
>Data una sequenza di simboli $c_{1}, . . . , c_{n} \in \Sigma$, definiamo: $w := c_{1} . . . c_{n}$ come stringa (o parola) di $\Sigma$.
>
>***Esempio:*** Dato l’alfabeto $\Sigma = \{0, 1, x, y, z\}$, una stringa di $Simga$ è $0x1yyy0$.

>[!note] Definizione 3: Linguaggio 🟢
>
>Dato un alfabeto $\Sigma$, definiamo come linguaggio di $\Sigma$, indicato come $\Sigma^{*}$, l’insieme delle stringhe di $\Sigma$.

>[!note] Definizione 4: Lunghezza di una stringa 🟢
>
>Data una stringa $w \in \Sigma^{*}$, definiamo la lunghezza di $w$, indicata come $| w |$, come il numero di simboli presenti in $w$.

>[!note] Definizione 5: Concatenazione 🟢
>Data la stringa $x := x_{1} . . . x_{n} ∈ \sigma^{*}$ e la stringa $y := y_{1} . . . y_{m} \in \Sigma^{*}$, definiamo come concatenazione di $x$ con $y$ attraverso:
>
>$$
>xy = x \cdot y = x_{1} . . . x_{n}y_{1} . . . y_{m}
>$$

>[!warning] Proposizione 1: Stringa vuota 🟢
>
>Indichiamo con ε la stringa vuota, ossia l’unica stringa tale che:
>- $\mid \epsilon \mid = 0$
>- $\forall  w \in \Sigma^{*}\ \ w \cdot \epsilon = \epsilon \cdot w = w$
>- $\Sigma^{*} \not = \emptyset \implies \epsilon \in \Sigma^{*}$ (capire se $\Sigma^{*}$ è insieme delle parti di $\Sigma$ perché se è cosi ha senso)

>[!note] Definizione 6: Conteggio 🟢
>Data una stringa $w \in \Sigma^{*}$ e un simbolo $a \in \Sigma$ definiamo il conteggio di $a$ in $w$, indicato come $|w|_{a}$, il numero di simboli uguali ad $a$ presenti in $w.$

>[!note] Definizione 7: Stringa rovesciata 🟢
>
>Data una stringa $w = a_{1} ...a_{n} \in \Sigma^{*}$, dove $a_{1}...a_{n} \in \Sigma$, definiamo la sua stringa rovesciata, indicata con $w^{R}$ come $w^{R} = a_{n}...a_{1}$

>[!note] Definizione 8: Potenza 🟢
>
>Data la stringa $w \in \Sigma^{*}$ e dato $n\in \mathbb{N}$, definiamo come potenza la seguente operazione:
>
>$$
>w^{n} = \begin{cases}
>\ \epsilon & \text{ se }n = 0 \\
>\ w \cdot w^{n-1} & \text{ se } n> 0
>\end{cases}
>$$

>[!warning] Proposizione 2: Operazioni su lingiaggi 🟢
>
>Dati i linguaggi $L,L_{1},L_{2} \subseteq \Sigma^{*},$ definiamo le seguenti operazioni:
>
>**Operatore unione:**
>
>$$
>L_{1} \cup L_{2} = \{ w \in \Sigma^{*} \ :\ w \in L_{1} \vee  w \in L_{2} \}
>$$
>
>**Operatore intersezione:**
>
>$$
>L_{1} \cap L_{2} = \{w \in  \Sigma^{*}\ :\ w \in L_{1}\ \wedge  w \in L_{2} \}
>$$
>
>**Operatore complemento:**
>
>$$
>\overline{L} = \{w \in \Sigma^{*} \ :\ w \not \in L \}
>$$
>
>**Operatore concatenazione:**
>
>$$
>L_{1} \circ L_{2} = \{ xy\ : \ x \in L_{1} \wedge y \in L_{2} \}
>$$
>
>**Operatore potenza:**
>
>$$
>L^{n} = \begin{cases}
>\ \{ \epsilon \} & \text{se } n=0 \\
>\ L \circ L^{n-1} & \text{se } n>0
>\end{cases}
>$$
>
>**Operatore star di Kleene:**
>
>$$
>L^{*} = \bigcup_{n\geq 0} L^{n}
>$$
>
>>*esempio:* $L = \{ a,b \}$ allora $L^{*} = \{ \epsilon, \, a,\, b,\, aa,\, ab,\, bb,\, ba,\, aaa,\, \dots \}$
>
>**Operatore plus di Kleene:**	
>
>$$
>L^{+} = \{  \}
>$$

>[!danger] Teorema 1: Leggi di Demorgan 🟢
>
>Dati due linguaggi $L_{1}$ e $L_{2}$, si ha che:
>$$
>L_{1} \cup L_{2} = \overline{\overline{L_{1}} \cap \overline{L_{2}}}
>$$
>
>$$
>L_{1} \cap  L_{2} = \overline{\overline{L_{1}} \cup  \overline{L_{2}}}
>$$
>
>(dimostrazione omessa)
