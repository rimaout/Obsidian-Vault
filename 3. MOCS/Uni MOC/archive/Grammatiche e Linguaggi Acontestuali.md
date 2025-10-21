---
type: Uni Note
class:
  - "[[Automi (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-10-15T14:35
updated: 2025-10-21T10:52
---
## Introduzione

Introduciamo un modello di grammatica chiamata ***context free grammar*** che crea nuovi tipi di automi capaci di riconoscere anche linguaggi non regolari (quindi non ottenibili attraverso automi finiti e espressioni regolari) come ad esempio $\{ 0^{n}1^{n} \mid n\geq 0 \}$.

In particolare queste grammatiche sono molto utili nel ambìto della specifica dei **parser** dei linguaggi di programmazione, utilizzati nei compilatori ed interpreti.

I linguaggi associati alle grammatiche context free, sono detti ***linguaggi context free***, questa classe di linguaggi contiene tutti i linguaggi regolari e molti ulteriori linguaggi.

Infine vedremo gli **automi a pila** (pushdown automata) una classe di automi che riconosce i linguaggi context free.

## Definizioni di gramatica (CFG)

>[!note] Definizione: Context-free Grammar (CFG)
>
>Una **Context-free Grammar (CFG)** è una quadrupla $(V, \Sigma, R, S)$ dove:
>- $V$ è l’insieme delle *variabili* della grammatica
>- $\Sigma$ è l’insieme dei *terminali* della grammatica
>- $R$ è l’insieme delle *regole* o *produzioni* della grammatica
>- $S \in V$ è la *variabile iniziale* della grammatica
>
>>***Nota*** che $V \cap \Sigma = \emptyset$, ossia variabili e terminali sono tutti distinti tra loro
>
>Le **regole** in $R$ assumono la forma $A → X$, dove $A \in V$ , ossia è una variabile, e $X \in (V \cup \Sigma_{\epsilon})^{*}$, ossia è una stringa composta da una o più variabili e/o terminali.

>[!example]- Esempio
>
>La tupla $G = \big( \{ A, B \}, \{ 0, 1, \# \}, R, A \big)$ è un ***CFG*** dove in $R$ sono definite le seguenti regole.
>
>Regole della grammatica sono:
>- `R1`: $A \to 0A1$
>- `R2`: $A \to B$
>- `R2`: $B \to \#$
>
>Dove:
>- $0,1,\#$ sono detti terminali
>- $A$ e $B$ sono dette variabili

^3303ff

>[!warning] Acontestualità
>
>L'acontestualità è la condizione secondo cui il lato sinistro delle regole della grammatica è composto sempre e solo da una singola variabile, ad esempio:
>- La regola `A → B` può appartenere ad una CFG
>- La regola `AB → B` non può appartenere ad una CFG

>[!warning] Notazione compatta per le regole
>
>Data una CFG $G = \big( V,\Sigma ,R,S \big)$, se in `R` esistono più regole $A \to X_{1},X_{2},\dots, A \to X_{n}$ definite sulla stessa variabile $A$, è possibile indicare tali regole con la seguente notazione contratta:
>
>$$
>A \to  X_{1} \mid X_{2} \mid \dots \mid X_{n}
>$$
>
>**Esempio:** Le regole della CFG dell’[[#^3303ff|esempio precedente]] possono essere contratte in:
>
>- $A \to  0A1 \mid B$
>- $B \to \#$

## Produzione  e Derivazione

>[!note] Produzione
>
>Se `u`, `v`, `w` sono stringhe di variabili o terminali ed esiste la regola $A \to w$, allora la stringa `uAv` produce la stringa `uwv`, denotato come $uAv ⇒ uwv$.

>[!note] Creazione di stringhe
>
>Dato un CFG e una *variabile iniziale* è possibile utilizzare le *regole di sostituzione* per generare delle stringhe, in particolare:
>
>**Procedimento:** La grammatica genera stringhe, seguendo questo processo:
>1. Presa la variabile iniziale
>2. Sostituisco le variabili con altre variabili o terminali, seguendo le regole della grammatica
>3. Ripeto `step 2` fino a che non ho più variabili
>   
>>***Esempio:*** utilizzando il CFG dell'[[#^3303ff|esempio precedente]] è possibile produrre la stringa $000\#111$, dove:
>>- le *regole* utilizzate  sono: $A \to  0A1 \mid B$, $B \to \#$
>>- la *serie di produzioni* (derivazione) utilizzata è: $000\#111$ è $A\implies 0A1\implies 00A11\implies 000A111\implies 000\#111$

>[!note] Albero Sintattico
>
>Ogni produzione può essere rappresentata mediante un albero sintattico (parser tree).
>
>>***Esempio:*** l'albero sintattico della produzione precedentemente vista è:
>>
>>![[Pasted image 20251020111403.png|500]]

>[!note] Derivazione
>
>Una sequenza di sostituzioni utilizzate per ottenere una stringa attraverso un CFG è detta derivazione.
>
>Più **formalmente** sia $G = \big( V, \Sigma, R,S \big)$ una CFG, date $u,v \in \big(V\cup\Sigma\big)^{*}$, diciamo che `u` deriva `v`, denotato come $U \overset{*}{\Rightarrow} v$, se $u = v$ oppure se $\exists u_{1},\dots, u_{k} \in \big(V \cup \Sigma \big)^{*}$ tali che:
>
>$$
>u \Rightarrow u_{1} \Rightarrow \dots \Rightarrow u_{k} \Rightarrow u
>$$
>
>>***Esempio:*** utilizzando il CFG dell'[[#^3303ff|esempio precedente]] abbiamo che la stringa $000\#111$ è derivata da $A$, quindi $A \overset{*}{\Rightarrow} 000\#111$.
>
>

>[!warning] Notazione
>
>Quindi $\Rightarrow$ e $\overset{*}{\Rightarrow}$ hanno significati simili ma:
>- $\Rightarrow$ indica una singola applicazione di una regola di sostituzione, ad esempio $A \Rightarrow 0A1$
>- $\overset{*}{\Rightarrow}$ indica una sequenza di sostituzioni, ad esempio $A \overset{*}{\Rightarrow} 000\#111$

## Linguaggi Acontestuali (CFL)

Sia $G = \big( V, \Sigma, R, S \big)$ un CFG, il **context-free Language (CFL)** generata da $G$ è indicato da $L(G)$, ed è l’insieme di stringhe derivate dalle regole di $G$ tramite $S$.
$$
L(G) = \{ w \in \Sigma^{*} \mid S \overset{*}{\Rightarrow} w \}

$$

>[!example]- Esempi
>
>**Esempio 1)**
>
>Dato il CFG $G = \big( \{ S \},\, \{ a,b \},\, R,\, S\, \big)$, dove:
>
>$$
>S \to  \epsilon \mid aSb \mid SS
>$$
>
>Si ha che:
>- $S \Rightarrow aSb \Rightarrow a\epsilon b = ab, \text{ dunque } ab \in L(G)$
>- $S \Rightarrow aSb \Rightarrow aaSbb \Rightarrow aa\epsilon bb = aabb, \text{ dunque } aabb \in L(G)$
>- $S \Rightarrow SS \overset{*}{\Rightarrow} aSbaSb \overset{*}{\Rightarrow} a\epsilon ba\epsilon b = abab,\text{ dunque } abab \in L(G)$
>- $\dots$
>
>---
>**Esempio 2)**
>
>Dato il linguaggio:
>
>$$
>L_{2}= \{ w \in \{ 0,1 \}^{*} \mid |w|_{1} \geq 3 \}
>$$
>
>Un CFG $G$ che che genera $L_{2}$ (ovvero $L(G) = L_{2}$) è $G = \big( \{ S,T \},\, \{ 0,1 \},\, R,\, S\, \big)$, dove:
>- $S \to T1T1T1T$
>- $T \to \epsilon \mid 0T \mid 1T$
>
>>*Nota:* $|w|_{1}\geq 3$ indica che il numero di 1 nella stringa deve essere maggiore uguale di 3.
>
>---
>**Esempio 3)**
>
>Dato il linguaggio:
>
>$$
>L_{3} = \{ w \in \{ 0,1 \}^{*} \mid w = w^{R} \wedge |w| \text{ è pari} \}
>$$
>
>Un CFG $G$ che genera il linguaggio (ovvero $L(G) = L_{3}$) è $G = \big( \{ S\},\, \{ 0,1 \},\, R,\, S\, \big)$, dove:
>- $S \to \epsilon \mid 0S0 \mid 1S1$
>
>---
>**Esempio 4)**
>
>Dato il linguaggio:
>
>$$
>L_{4} = \{ a^{i} b^{j} c^{i+j} \in \Sigma^{*} \mid i,j \in \mathbb{N} \}
>$$
>
>Un CFG $G$ che genera il linguaggio (ovvero $L(G) = L_{4}$) è $G = \big( \{ S \},\, \{ a,b \},\, R,\, S\, \big)$, dove:
>
>- $S \to aSc \mid T$
>- $T \to bTc \mid \epsilon$

## Ordine di derivazione e grammatiche ambigue


>[!note] Osservazione: Più derivazioni per una stessa stringa
>
>Sia $G$ una CFG. Data la stringa $w \in L(G),$ possono esistere più derivazioni di $w$
>
>---
>
>**Esempio:**
>
>

Alta grammatica:
$$
\begin{align*}
&(R_{1})\ \ \ E \to  E + E\\
&(R_{2})\ \ \ E \to  E * E\\
&(R_{3})\ \ \ E \to  E + (E)\\
&(R_{4})\ \ \ E \to  0|1|2|\dots|9
\end{align*}
$$




