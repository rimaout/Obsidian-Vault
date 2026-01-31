---
type: Uni Note
class:
  - "[[Automi (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-10-03T14:14
updated: 2026-01-31T13:32
---
## Teorema

Vedremo che gli automi a stati finiti deterministici e quelli non deterministici riconoscono la stessa classe di linguaggi. Questo è estremamente utile perché a volte è molo più semplice descrivere un NFA che un DFA per un dato linguaggio.

>[!danger] Teorema: Equivalenza tra NFA e DFA
>
>Date le due classi dei linguaggi $\mathcal{L}(DFA)$ e $\mathcal{L}(NFA)$, si ha che:
>
>$$
>\mathcal{L}(DFA) = \mathcal{L}(NFA)
>$$
>
>Dove dato un alfabeto $\Sigma$, definiamo:
>- La classe dei linguaggi di $\Sigma$ riconosciuti da un NFA il come: $\mathcal{L}(NFA) = \big\{\mathcal{L} \subseteq \Sigma^{*}\ |\ \exists\; \text{NFA}\ N \text{ t.c } \mathcal{L}= \mathcal{L}(N)\big\}$
>- La classe dei linguaggi di $\Sigma$ riconosciuti da un DFA il come: $\mathcal{L}(DFA) = \big\{\mathcal{L} \subseteq \Sigma^{*}\ |\ \exists\; \text{DFA}\ D \text{ t.c } \mathcal{L}= \mathcal{L}(D)\big\}$

## Dimostrazione

Il nostro obbiettivo è dimostrare che: $\mathcal{L}(\text{DFA}) \subseteq \mathcal{L}(\text{NFA}) \iff \mathcal{L}(\text{NFA}) \subseteq \mathcal{L}(\text{DFA})$:

>[!note] Prima implicazione
>
>**Obbiettivo:** $\mathcal{L}(\text{DFA}) \subseteq \mathcal{L}(\text{NFA})$
>
>Dato $L \in \mathcal{L}(\text{DFA})$, sia $D := (Q,\Sigma,\delta,q_{0},F)$ il DFA tale che $L= L(D)$
>
>Poiché il concetto di NFA è una generalizzazione del concetto di DFA, ne segue automaticamente che $D$ sia anche un NFA, implicando che $L \in \mathcal{L}(\text{NFA})$ e di conseguenza che:
>
>$$
>\mathcal{L}(\text{DFA}) \subseteq \mathcal{L}(\text{NFA})
>$$

>[!note] Seconda implicazione
>
>**Obbiettivo:** $\mathcal{L}(\text{NFA}) \subseteq \mathcal{L}(\text{DFA})$
>
>Dato $L \in \mathcal{L}(\text{NFA})$, sia $N:= (Q_{N}, \Sigma, \delta_{N},q_{0_{N}}, F_{N})$ in NFA tale che $L = L(N)$
>
>Consideriamo il DFA $D := (Q_{D},\Sigma, \delta_{D},q_{0_{D}},F_{D})$ costruito tramite `N` stesso, ovvero tale che:
>
>>Gli **stati** di $D$ sono $Q_{D} = \mathcal{P}(Q_{N})$
>>
>>Quindi:
>>- $D$ contiene uno stato per ogni possibile combinazioni di stato in $N$
>>- se $k$ è in numero di stati di $N$ allora $2^{k}$ è il numero di stati di $D$
>  
>>Definiamo come **estensione** di uno stato di $N$ come: 
>>$$
>>E(R) = \{ q \in Q_{N}\ |\ q \in R\ \vee \ q\ \text{può essere raggiunto partendo da }R\text{ utilizzando un }\epsilon \text{ -arco} \}
>>$$
>>
>>Dove `R` è uno stato di `D`, ovvero $R \in Q_{D}$ 
>>
>>***Nota:*** $E(R)$ nel contesto di `D` è uno stato singolo e non un insieme di stati
>
>>Lo **stato iniziale** di $D$ è $q_{0_{D}} = E\big( \{ q_{0_{N}} \} \big)$
>
>>Gli **stati di accettazione** di $D$ sono $F_{D} = \{ R \in Q_{d}\, \mid \, R \cap F_{N} \not= \emptyset \}$
>>
>>Quindi l'insieme degli stati di accettazione contiene tutti gli stati di `D` tale che ognuno di questi contiene al suo interno almeno uno stato di accettazione di `N`
>
>>La **funzione di transizione** di `D` è definita come:
>>
>>$$
>>\delta_{D}(R,a) = \bigcup_{r \in R} E\big(\delta_{N}(r,a)\big)
>>$$
>>
>>Dove $R\in Q_{D}$ e $a \in \Sigma$
>
>A questo punto, per costruzione stessa di D si ha che:
>
>$$
>w \in L \iff w \in L(D)
>$$
>
>Quindi abbiamo ottenuto che:
>
>$$
>\mathcal{L}(\text{NFA}) \subseteq \mathcal{L}(\text{DFA})
>$$
>
>***Nota:*** in questa dimostrazione gli stati di $D$ sono composti da insiemi di stati di $N$

## Travare DFA equivalente a NFA

Dato un NFA `N` , seguendo i passaggi della dimostrazione precedente è possibile definire un DFA `D` equivalente ad `N`.

>[!example] Esempio
>
>Consideriamo il seguente NFA, proviamo a trovare il DFA $D$ equivalente.
>
>![[Pasted image 20251007122315.png|350]]
>
>Definiamo quindi l’insieme degli stati del DFA equivalente a tale NFA:
>
>$$
>Q_{D} = \big{\{} \emptyset,\, \{q_{1}\},\, \{q_{2}\},\, \{q_{3}\},\, \{ q_{1},q_{2}\},\, \{ q_{1},\, q_{3} \},\, \{ q_{2},q_{3}  \}, \{q_{1},q_{2},q_{3}\} \big{\}}
>$$
>
>Per facilitare la lettura, riscriviamo i vari stati con la seguente notazione:
>
>$$
>Q_{D} = \{ \emptyset,\, q_{1},\, q_{2},\, q_{3},\, q_{1,2},\, q_{1,3}\, ,q_{2,3},\, q_{1,2,3} \}
>$$
>
>A questo punto, poniamo :
>- $q_{0_{D}} = E(\{q_{0_{N}} \})$ = $E(\{ q_{1} \}) = \{ q_{1},q_{3} \} = q_{1,3}$
>- $F_{D} = \{ q_{1},q_{1,2},q_{1,3},q_{1,2,3} \}$
>  
>La funzione di transizione del DFA corrisponde a:
>- $\delta_{D}(q_{1}, a) = E\big(\delta_{N}(q_{1},a)\big) = \emptyset$
>- $\delta_{D}(q_{1}, b) = E\big(\delta_{N}(q_{1},b)\big) = q_{2}$
>- $\delta_{D}(q_{2}, 1) = E\big(\delta_{N}(q_{2},a)\big) = q_{2,3}$
>- $\delta_{D}(q_{2}, b) = E\big(\delta_{N}(q_{2},b)\big) = q_{3}$
>- $\delta_{D}(q_{3}, a) = E\big(\delta_{N}(q_{3},a)\big) = q_{1,3}$
>- $\delta_{D}(q_{3}, b) = E\big(\delta_{N}(q_{3},b)\big) = q_{3}$
>- $\delta_{D}(q_{1,2}, a) = E\big(\delta_{N}(q_{1},a)\big) \cup E\big(\delta_{N}(q_{2},a)\big) = \emptyset \cup q_{2,3} = q_{2,3}$
>- $\delta_{D}(q_{1,2}, b) = E\big(\delta_{N}(q_{1},b)\big) \cup E\big(\delta_{N}(q_{2},b)\big) = q_{2} \cup q_{3} = q_{2,3}$
>  
>>***Nota:*** data la nostra notazione $\emptyset \cup q_{2,3}$ equivale a $\emptyset \cup \{ q_{2}, q_{3} \}$
>
>Quindi il DFA equivalente corrisponde a:
>
>![[Pasted image 20251009123105.png|700]]
>![[Pasted image 20251009132045.png|700]]

