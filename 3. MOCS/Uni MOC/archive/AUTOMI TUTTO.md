---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2026-09-25T12:49
updated: 2026-09-28T14:29
---
>[!note] Definizione 1 - Deterministic Finite Automata (DFA)
>
>Un **DFA** $D$ è definito come una quintupla $D = (Q, \Sigma, \delta, q_{0}, F)$ dove:
>- $Q$ è l'insieme finito degli stati
>- $\Sigma$ è l'alfabeto (insieme finito e non vuoto di simboli in input)
>- $q_{0} \in Q$ è lo stato iniziale
>- $F \subseteq Q$ è l'insieme degli stati accettanti (o finali)
>
>La **Funzione di Transizione** $\delta$, ci dice come avvengono i passaggi di stato, è definita come:
>$$
>\delta : Q \times \Sigma \to Q
>$$
>
>La **Funzione di Transizione Estesa** $\delta^{*}$, permette di dare in input all'automa una stringa intera (invece di un carattere alla volta), è definita induttivamente come:
>- $\delta^{*}(q,\epsilon) = q$
>- $\delta^{*}(q,aw) = \delta^{*}(\delta(q,a), w)$
>
>Una stringa $w \in \Sigma^{*}$ si dice **Accettata** dal DFA se: 
>$$\delta^{*}(q_{0},w) \in F$$
>
>Il **Linguaggio Riconosciuto** dal DFA $D$, indicato con $L(D)$, è definito come:
>$$L(D) = \{ w \in \Sigma^{*} : \delta^{*}(q_{0},w) \in F \}$$
>
>La **Classe dei Linguaggi Riconosciuti** dai DFA è definita come:
>$$
>{\cal L}(DFA) = \{ L \in \Sigma^{*} : \exists D\ DFA \wedge L(D) = L\}
>$$

>[!note] Definizione 2 - Non-Deterministic Finite Automaton (NFA)
>
>Un **NFA** $N$ è definito come una quintupla $N = (Q, \Sigma, \delta, q_{0}, F)$ dove tutti gli elementi sono come per i DFA ma abbiamo un cambio nella **Funzione di Transizione**:
>
>$$
>\delta : Q \times \Sigma_{\epsilon} \to \mathcal{P}(Q)
>$$
>
>Dove:
>1. $\mathcal{P}(Q)$ è l’insieme delle parti i $Q$ ovvero l’insieme di tutti i possibili sottoinsiemi di $Q$
>2. $\Sigma_{\epsilon} = \Sigma \cup \{ \epsilon \}$
>  
>Questo ha due implicazioni importanti:
>1. Per uno stessa configurazione in input (stato, carattere) sono percorribili più archi che verranno eseguiti in modo parallelo e indipendente.
>2. Se è presente le funzione $\delta(q_{1},\epsilon) = q_{2}$ significa che l'automa può percorrere il larco $q_{1} \to q_{2}$ senza consumare nessun carattere in input.
>
>Quindi è possibile visualizzare il composrtamento di un NFA attraverso l'**Albero di Computazione** ...
>
>Boh forse scrivere tipo questo: Per quanto riguarda gli ε-archi invece, se l’automa si trova in uno stato che ne possiede uno allora l’automa si duplica in due rami senza leggere nessun input: • Un ramo rimane nella stessa configurazione di prima. • L’altro ramo segue l’ε-arco.
>
>La funzione di tranziozione estesa ...
>
>Una stringa si dice **Accettata** da ....

>[!note] Definizione 2: Non-Deterministic Finite Automaton (NFA / $\epsilon$-NFA)
>
>Un **NFA** $N$ è definito come una quintupla $N = (Q, \Sigma, \delta, q_{0}, F)$ dove $Q, \Sigma, q_0, F$ mantengono lo stesso significato del DFA, ma la **Funzione di Transizione** è definita come:
>$$
>\delta : Q \times \Sigma_{\epsilon} \to \mathcal{P}(Q)
>$$
>Dove:
>- $\mathcal{P}(Q)$ è l'**insieme delle parti** di $Q$ (l'insieme di tutti i possibili sottoinsiemi di $Q$).
>- $\Sigma_{\epsilon} = \Sigma \cup \{ \epsilon \}$, ovvero l'alfabeto esteso con il simbolo di stringa vuota $\epsilon$.
>
>Il **Non-Determinismo** è dovuto a:
>- *Moltitudine di scelte*: Per una stessa coppia $(\text{stato}, \text{simbolo})$, l'automa può passare a un insieme di stati possibili (anche vuoto, $\emptyset$).
>- *Epsilon-transizioni*: Se $\delta(q_1, \epsilon)$ contiene $q_2$, l'automa può passare da $q_1$ a $q_2$ senza consumare alcun carattere in input.
>
>*(Intuizione: È possibile visualizzare il comportamento di un NFA come un **albero di computazione**, in cui ogni scelta non deterministica o $\epsilon$-arco genera una ramificazione parallela. Se almeno un ramo giunge a uno stato finale a fine input, la computazione ha successo).*
>
>---
>
>### $\epsilon$-Chiusura ($\epsilon$-closure)
>Per ogni stato $q \in Q$, la $\epsilon$-chiusura $ECLOSE(q) \subseteq Q$ è l'insieme di tutti gli stati raggiungibili da $q$ percorrendo **zero o più** $\epsilon$-transizioni.
>
>### Funzione di Transizione Estesa
>La funzione $\delta^* : Q \times \Sigma^* \to \mathcal{P}(Q)$ calcola l'insieme degli stati raggiungibili a partire da uno stato $q$ leggendo un'intera stringa $w$. È definita induttivamente per ogni $q \in Q$, $w \in \Sigma^*$ e $a \in \Sigma$ come:
>- $\delta^*(q, \epsilon) = ECLOSE(q)$
>- $\delta^*(q, wa) = ECLOSE\left( \bigcup_{p \in \delta^*(q, w)} \delta(p, a) \right)$
>
>---
>
>### Accettazione e Linguaggio
>Una stringa $w \in \Sigma^*$ si dice **Accettata** dal NFA se la computazione termina con **almeno uno** stato accettante:
>$$\delta^*(q_{0}, w) \cap F \neq \emptyset$$
>
>Il **Linguaggio Riconosciuto** dal NFA $N$, indicato con $L(N)$, è definito come:
>$$L(N) = \{ w \in \Sigma^* \mid \delta^*(q_{0}, w) \cap F \neq \emptyset \}$$

>[!danger] Teorema 1: ${\cal L}(DFA) = {\cal L}(NFA)$
>
>Dimostrazione - Formalmente vogliamo dimostrare ${\cal L}(DFA) \subseteq {\cal L}(NFA)$ e ${\cal L}(NFA) \subseteq {\cal L}(DFA)$.
>
>**Prima Implicazione ${\cal L}(DFA) \subseteq {\cal L}(NFA)$: **
>
>
>
>**Seconda Implicazione ${\cal L}(NFA) \subseteq {\cal L}(DFA)$:**
>
>
