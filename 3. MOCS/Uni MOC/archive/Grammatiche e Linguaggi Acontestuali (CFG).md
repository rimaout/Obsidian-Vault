---
type: Uni Note
class:
  - "[[Automi (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-10-15T14:35
updated: 2025-10-22T15:50
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

## Ambiguità e Ordine di Derivazione 

Alcune grammatiche possono **generare la stessa stringa in più modi diversi**, una tale stinga avrà diversi alberi sintattici e di conseguenza diversi significati.

Questa caratteristica in alcuni contesti può essere considerata indesiderata, ad esempio nei linguaggi di programmazione ogni programma deve avere un unica implementazione.

>***Ad esempio:*** se prendiamo un CFG con le seguenti regole: $E \to E+E  \mid E E \mid (E) \mid a$ 
>
>La stringa $a+a \times a$ può essere ottenuta in due modi:
>
>![[Pasted image 20251022092227.png|700]]

In particolare una **stinga genera ambiguità** quando ha più di un albero sintattico, e non più differenti derivazioni. Infatti una stinga non ambigue può avere due derivazioni che differiscono nell'ordine delle sostituzioni, ma non nell struttura complessiva.

Per definire formalmente il concetto di ambiguità, dobbiamo prima di tutto definire una derivazione a sinistra.

>[!note] Def: Derivazione a sinistra
>
>Data una CFG $G = \big(V, \Sigma, R, S\big)$, definiamo la derivazione $S \overset{*}{\Rightarrow} w$ come derivazione sinistra se ad ogni produzione interna alla derivazione viene valutata la variabile più a sinistra.
>
>>[!example]- Esempio
>>
>>Riprendiamo la CFG dell’esempio precedente, ma riscriviamo le regole per renderlo più leggibile (rimane equivalente):
>>- $E \to E+F \mid E \times E \mid (E) \mid a$
>>- $F \to E$
>>
>>Una derivazione sinistra della stringa $a + a + a$ corrisponde a:
>>
>>$$
>>E\ \Rightarrow \ E+F\ \Rightarrow \ E+F+F \ \Rightarrow \ a+F+F \ \Rightarrow \ a+E+F \ \Rightarrow \ a+a+F \ \Rightarrow \ a+a+E \ \Rightarrow \ a+a+a
>>$$

>[!note] Def: Grammatica ambigua
>
>Definiamo una grammatica $G$ come **ambigua** se $\exists w \in L(G)$ tale che esistono almeno due derivazioni a sinistra per $w$.

Se abbiamo una grammatica ambigua, a volte è possibile trovare una grammatica non ambigua che genera lo stesso linguaggio.

Tuttavia alcuni linguaggi context-free possono essere generati solo da grammatiche ambigue e vengono chiamati **linguaggi intrinsecamente ambigui**.

## Progettazione di CFG

Costruire grammatiche context-free è più complesso rispetto a creare degli automi finiti.

Ora vedremo delle tecniche che utilizzate singolarmente o combinate, aiutano nella creazione di grammatiche context-free.

>[!note] Unione tra CFL
>
>Molto CFG sono l'unione di CFG più semplici.
>
>---
>
>**Esempio:** Per ottenere una grammatica che descrive il seguente linguaggio:
>
>$$
>\{ 0^{n}1^{n} \mid n\geq 0 \} \cup  \{ 1^{n}0^{n} \mid n\geq 0 \}
>$$
>
>Troviamo prima la gramatica $s_{1} \to 0S_{1}1 \mid \epsilon$ per il linguaggio $\{ 0^{n}1^{n} \mid n\geq 0 \}$.
>
>Poi troviamo la grammatica $s_{2} \to 1S_{2}0 \mid \epsilon$ per il linguaggio $\{ 1^{n}0^{n} \mid n\geq 0 \}$
>
>Ora possiamo unire le grammatiche aggiungendo la regola $S \to S_{1} \mid S_{2}$, per ottenere un CFG che descrive il linguaggio $\{ 0^{n}1^{n} \mid n\geq 0 \} \cup  \{ 1^{n}0^{n} \mid n\geq 0 \}$.
>
>- $S \to S_{1} \mid S_{2}$
>- $s_{1} \to 0S_{1}1 \mid \epsilon$
>- $s_{2} \to 1S_{2}0 \mid \epsilon$

>[!note] Grammatiche con "Memoria"
>
>Alcuni linguaggi context-free contengono delle stringhe con due sottostringhe che sono "collegate" tra loro, ovvero sottostringhe dove il numero di caratteri di una dipende dal numero di caratteri dell'altra.
>
>Ad esempio il linguaggio $\{ 0^{n}1^{2n} \mid n\geq 0 \}$ per essere riconosciuto dobbiamo avere una grammatica capace di ricordare il numero di simboli uguali a 0 per verificare che esso è uguale al numero di simboli uguali a 1.
>
>Si può costruire un CFG per gestire questa situazione usando la regola della forma $R \to 0R11$

## Linguaggi acontestuali ad estensione dei regolari

>[!note] Classe dei linguaggi acontestuali
>Dato un alfabeto Σ, definiamo come classe dei linguaggi acontestuali di Σ il seguente insieme:
>
>$$
>\text{CFL} = \big\{\,L \subseteq  \Sigma^{*} \mid \exists \text{CFG }\, G\ \text{ t.c }\ L = L(G)\, \big\}
>$$

>[!danger] Lemma: Conversione da DFA a CFG
>Date le due classi dei linguaggi REG e CFL, si ha che: 
>$$
>\text{REG} \subset  \text{CFL}
>$$

>[!note] Costruire CFG partendo da DFA
>
>Se si deve costruire un CFG per un linguaggio regolare allora è possibile costruire prima un DFS per quel linguaggio. 
>
>Poi possiamo trasforma il DFA in un CFG equivalente, in questo modo:
>- Creiamo una variabile $R_{i}$ per ogni stato $q_{i}$ del DFA
>- Aggiungiamo la regola $R_{i} \to aR_{j}$ se $\delta(q_{i},a) = q_{j}$ è una transazione del DFA
>- Aggiungiamo la regola $R_{i} \to \epsilon$ se $q_{i}$ se $q_{i}$ è uno stato accettante del DFA
>- Assumiamo che $R_{0}$ è la variabile iniziale, dove $q_{0}$ è lo stato iniziale della macchina.
>  
>È possibile verificare che i linguaggi del DFA e CFG sono equivalenti.

>[!example] Esempio
>
>Consideriamo il seguente DFA:
>
>![[Pasted image 20251022153826.png|800]]
>
>Un CFG $G = \big( V,\Sigma, R, S \big)$ equivalente è sostituito da:
>- $V = \{ V_{1},V_{2},V_{3},V_{4} \}$
>- $S = V_{1}$
>- $R$ definito come:
>
>$$
>\begin{align*}
>& V_{1} \to  0V_{1} \mid 1V_{2}\\
>& V_{2} \to  0V_{2} \mid 1V_{3}\\
>& V_{3} \to  0V_{3} \mid 1V_{4}\\
>& V_{4} \to  0V_{4} \mid 1V_{4} \mid \epsilon
>\end{align*}
>$$
>
>Sia il DFA che il CFG descrivono il linguaggio:
>
>$$
>L = \{ w \in \Sigma^{*} \mid |w|_{1}\geq 3 \}
>$$
