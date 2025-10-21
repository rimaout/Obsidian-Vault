---
type: Uni Note
class:
  - "[[Automi (class)]]"
academic year: 2024/2025
related:
completed: false
created: 2025-10-10T12:14
updated: 2025-10-16T17:15
---
## Definizione

I GNFA sono dei NFA nei quali gli archi delle transazioni possono avere espressioni regolari come etichette, invece che solo elementi dell'alfabeto o $\epsilon$.
 
Il GNFA legge blocchi di simboli dall'input, non necessariamente un singolo carattere alla volta.

Infatti il GNFA si muove lungo un arco di transizione che collega due stati quando legge dall'input un blocco di simboli che formano una stringa descritta dall'espressione regolare su quell'arco.

>[!note] Definizione Formale
>
>Un **Generalized NFA (GNFA)** è una quintupla $\big(Q,\, \Sigma,\, \delta,\, q_{\text{start}},\, q_{\text{accept}}\big)$ dove:
>- $Q$ è l'insieme (finito) degli stati dell'automa dove $|Q| \geq 2$
>- $\Sigma$ è l'alfabeto dell'automa
>- $q_{\text{start}} \in Q$ è lo stato iniziale
>- $q_{\text{accept}} \in Q$ è l'*unico* stato di accettazione
>  
>La funzione di transizione dell'automa è definita cosi:
>
>$$
>\delta: \big( Q-\{ q_{\text{accept}} \}\big) \times \big( Q - \{ q_{\text{start}} \}\big) \to re(\Sigma)
>$$
>
>Questa definizione implica che:
>- Lo stato $q_{\text{start}}$ ha solo transizioni *uscenti*
>- Lo stato $q_{accept}$ ha solo transizioni *entranti*
>- Per tutte le possibili coppie di stati $q,q_{1} \in Q$ (incluso $q = q'$) si ha la transizione $q \to q'$ e $q' \to q$
>- Le "etichette" delle transizioni sono delle espressioni regolari

>[!warning] ø -> transizione non utilizzabile
>
>Una transizione con "etichetta" pari a $\emptyset$ è una transizione inutilizzabile in quanto $L(\emptyset) = \emptyset$

>[!example]- Esempio
>
>![[Pasted image 20251010132203.png|650]]

## Classe di linguaggi riconosciuti da un GNFA

Dato un alfabeto $\Sigma$, definiamo come classe dei linguaggi di $\Sigma$ riconosciuti da un GNFA il seguente insieme:

$$
\mathcal{L}(\text{GNFA}) = \big\{ L \subseteq \Sigma^{*} \mid \exists\ \text{GNFA}\ G \text{ t.c } L = L(G) \big\}
$$

>[!note] Lemma: Conversione da DFA a GNFA
>
>Data due classi dei linguaggi $\mathcal{L}(\text{DFA})$ e $\mathcal{L}(\text{GNFA})$, si ha che:
>
>$$
>\mathcal{L}(\text{DFA}) \subseteq \mathcal{L}(\text{GNFA})
>$$

>[!warning] Dimostrazione: Conversione da DFA a GNFA
>
>Dato $L \in \mathcal{L}(\text{DFA})$, sia $D:= \big( Q, \Sigma, \delta, q_{0}, F \big)$ il DFA tale $L(D) = L$
>
>Ora consideriamo il GNFA $G := \big( Q', \Sigma, \delta', q_{\text{start}}, q_{\text{accept}} \big)$ costruito tramite $D$ stesso:
>- $Q' = Q \cup \{ q_{\text{start}},q_{\text{accept}} \}$
>- $\delta'(q_{\text{start}}, q_{0}) = \epsilon$
>- $\forall q \in F\ \ \delta'(q,q_{\text{accept}}) = \epsilon$
>- per ogni transizione in $D$ ne creiamo una equivalente in $G$
>- ogni transizione di $G$ con etichetta "multipla" (es. $a,b$) viene sostituita da una transizione equivalete con etichetta corrispondente all'unione dei "componenti" dell'etichetta multipla (es, $a \cup b$)
>- per ogni coppia di stato per cui non esiste una transizione entrante o uscente in $D$, viene aggiunta una transizione con etichetta $\emptyset$.
>  
>A questo punto, per costruzione stesa di $G$ si ha che $w \in L(D) \implies w \in L(G)$ implicando dunque che $L(D) \in \mathcal{L}(\text{GNFA})$ e di conseguenza:
>
>$$
>\mathcal{L}{\text{DFA}} \subseteq \mathcal{L}(\text{GNFA})
>$$

>[!example] Esempio
>
>Esempio di un DFA e di un GNFA equivalente:
>
>![[Pasted image 20251010170029.png|1300]]

## Convertire GNFA in Espressione Regolare

Dato un GNFA $G = \big( Q,\Sigma,\delta,q_{\text{start}},q_{\text{accept}} \big)$ il seguente **algoritmo** permette di convertire $G$ in un nuovo GNFA equivalente a $G$, tale che è composto da due stati e un solo arco, dove l'etichetta del arco è l’espressione regolare $R$:

>Se `|G| == 2`, allora significa che `G` ha soltanto due stati $q_{\text{start}},q_{\text{accept}}$ e un solo arco che li collega
>
>Ritorna come espressione regolare `R` l'etichetta del unico arco di $G$
>

>Se `|G| > 2` scegliamo un qualsiasi stato $q_{\text{rip}} \in Q$ tale che $q_{\text{rip}} \not= q_{\text{start}}$ e $q_{\text{rip}} = q_{\text{accept}}$.
>
>Ora creiamo un GNFA $G' = \big( Q', \Sigma, \delta',q_{\text{start}}, q_{\text{accept}} \big)$ dove:
>
>- gli stati sono $Q' = Q - \{ q_{\text{rip}} \}$
>- la funzione di transizione $\delta'$ è definita in questo modo:
>
>$$
>\forall  a_{1}\in Q'-\{ q_{\text{accept}} \}, \ q_{j} \in Q' - \{  q_{\text{ start}} \} \text{, poniamo:}
>$$
>$$
>\delta(q_{i}, q_{j}) = (R_{1})(R_{2})^{*}(R_{3}) \cup (R_{4})
>$$
>
>Dove:
>- $R_{i} = \delta(q_{1}, q_{\text{rip}})$
>- $R_{2} = \delta(q_{\text{rip}}, q_{\text{rip}})$
>- $R_{3} = \delta(q_{\text{rip}}, q_{j})$
>- $R_{4} = \delta(q_{i}, q_{j})$
>  
>Una volta calcolato $G'$ riapplichiamo ricorsivamente l’algoritmo su di esso fino ad ottenere il caso `|G'| = 2`.

>[!warning] Dimostrazione Correttezza Algoritmo
>
>Dobbiamo dimostrare che il GNFA iniziale $G$, il GNFA finale ottenuta applicando l'algoritmo è equivalente a $G$.
>
>**Dimostrazione:**
>
>Sia $G_{0}, \dots, G_{n}$ la sequenza di GNFA prodotti dalla ricorsione dell'algoritmo, implicando che $G_{0} = G$ e $G_{n}$ sia l'output finale.
>
>Procediamo per induzione sul numero `k` di riduzioni, mostreremo che $L(G) = L(G_{0}) = \dots L(G_{n})$
>
>>**Caso Base:** se $k=0$, allora $G_{0} = G$, dunque $L(G) = L(G_{0})$
>
>>**Ipotesi Induttivo:** dato un $k$, assumiamo che per il GNFA $G_{k}:= \big( Q,\Sigma,\delta,q_{\text{start}},q_{\text{accept}} \big)$ si abbia che $L(G) = L(G_{k})$
>
>>**Passo Induttivo:** Consideriamo quindi il GNFA $G_{k+1} := \big( Q',\Sigma,\delta',q_{\text{start}},q_{\text{accept}} \big)$ ottenuto uno stato $q\in Q$ (ovvero $Q' = Q-\{ q \}$) e ponendo:
>>
>>$$
>>\delta'(q_{i}, q_{j} ) := \delta(q_{i}, q)\delta(q, q)^{*}\delta(q, q_{j} ) \cup  \delta(q_{i}, q_{j} )
>>$$
>>
>>Per ogni $q_{i} \in Q' - \{ q_{\text{accept}} \}$ e $q_{j} \in Q' - \{ q_{\text{start}} \}$
>>
>>Data una stringa $w:= w_{0}\dots w_{m} \in L(G_{k})$, esiste una sequenza di stati $q_{0},\dots,q_{m} \in W$ tali che:
>>- $q_{0} = q_{\text{start}}$ e $q_{m} = q_{\text{accept}}$
>>- $\forall i \in [0,m-1]\ w_{i} \in L \big( \delta (q_{i}, q_{i+1}) \big)$
>>  
>>A questo punto consideriamo la costruzione della funzione $\delta'$:
>>
>>$$
>>\delta'(q_{i},q_{j}) = \delta(q_{i}, q)\delta(q, q)^{*}\delta(q, q_{j} ) \cup  \delta(q_{i}, q_{j} )
>>$$
>>
>>- Se $q \in \{ q_{0},\dots,q_{m} \}$ allora tramite l'unione si ha che $w_{i} \in L\big( \delta(q_{i}, q_{j}) \big) \implies w \in L\big( \delta'(q_{i}, q_{j}) \big)$, dunque tutte le possibili sottostringhe passanti per le transizioni dirette da $q_{i}$ a $q_{j}$.


