---
type: Uni Note
class:
  - "[[Automi (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-09-25T16:48
updated: 2026-01-31T13:32
---
## Definizione

>[!note] Definizione: Automa 🟢
>
>Un automa è un meccanismo di controllo (o macchina) progettato per processare automaticamente una sequenza di input, mantenendo informazioni relative allo **stato** attuale dell’automa stesso ed agendo di conseguenza, **passando da uno stato all’altro**.

>[!note] Definizione: Deterministic Finite Automaton (DFA) 🟢
>
>Un Deterministic Finite Automaton (DFA) (o Automa Deterministico a Stati Finiti) è una quintupla $(Q,\Sigma,\delta,q_{0},F)$ dove:
>- $Q$ è l’insieme finito degli stati dell’automa
>- $\Sigma$ è l’alfabeto dell’automa
>- $\delta: Q \times \Sigma \to Q$ è la funzione di transizione degli stati dell’automa
>- $q_{0} \in Q$ è lo stato iniziale dell’automa
>- $F \subseteq Q$ è l’insieme degli stati accettanti dell’automa, ossia l’insieme degli stati su cui, a seguito della lettura di una stringa in input, l’automa accetta la corretta terminazione 
>
>**Funzione di transizione:** $\delta: Q \times \Sigma \to Q$ quindi dato un stato dell'automa e un simbolo in input la funzione ritorna lo stato che l'automa assume dopo la transizione.
>
>>[!example]- Esempio
>>
>>![[Pasted image 20250926122457.png|800]]
>>
>>Dove:
>> - $Q = \{ q_{0},q_{1},q_{2} \}$ è l'insieme degli stati dell'automa
>> - $q_{0}$ è lo stato iniziale
>> - $F = \{ q_{1} \}$ è l'insieme degli stati accettati
>> - $\Sigma = \{ 0,1 \}$ è l'alfabeto dell'automa
>> - $\delta:Q \times \Sigma \to Q$ è definita come:
>>
>>![[Pasted image 20251010121325.png|300]]
## Caratteristiche

>[!note] Definizione: Stato Pozzo 🟢
>
>Gli stati pozzo sono stati senza uscita, e (se non è anche uno stato di accettazione) indicano che la stringa su cui si sta applicando l'automa non raggiungerà mai uno stato di accettazione.

>[!note] Definizione: Funzione di transizione estesa 🟢
>
>Per definire precisamente il linguaggio di un automa dobbiamo introdurre la funzione di transizione estesa: 
>
>Sia $M := (Q,\Sigma,\delta,q_{0},F)$ un DFA, definiamo $\delta^{*} \ : \ Q \times\Sigma^{*} \to Q$ come funzione di transizione estesa di `M` la funzione ricorsivamente come:
>
>$$
>\begin{cases}
>&\delta^{*}(q, \epsilon) = \delta(q, \epsilon) = q\\
>&\delta^{*}(q, ax) = \delta^{*}(\delta(q,a), x)\ \text{ dove }\ x \in \Sigma^{*}, a \in \Sigma
>\end{cases} \\
>$$
>
>>[!example]- Esempio
>>
>>Utilizando l'esempio dell'automa visto precedentemente:
>>
>>$$
>>\delta^{*}(q_{0}, 100) = q_{1}
>>$$
>>
>>Dato che:
>>- $\delta(q_{0}, 1) = q_{1}$
>>- $\delta(q_{1}, 0) = q_{2}$
>>- $\delta(q_{2}, 0) = q_{1}$

>[!warning] Proposizione: Stringa accettata in un DFA 🟢
>
>Sia $M = (Q,\Sigma,\delta,q_{0},F)$ un DFA. Data una stringa $w \in \Sigma^{*}$, diciamo che `w` è accettata da `M` se $\delta^{*}(q_{0},w) \in F$, ossia l’interpretazione di tale stringa *termina su uno stato accettante*.

>[!note] Definizione: Linguaggio di un automa 🟢
>
>Se `M` è un DFA, l’insieme delle stringhe accettate da `M` è detto `L(M)`.
>
>$$
>L(M) = \{w \in \Sigma^{*}\ |\ M\text{ accetta }w\}
>$$
>
>Inoltre, diciamo che `M` riconosce` L(M)`

>[!note] Definizione: Configurazione 🟢
>
>Sia $M = (Q,\Sigma,\delta,q_{0},F)$ un DFA. Definiamo la coppia $(q,w) \in Q \times \Sigma^{*}$ come configurazione di `M`, quindi:
> - `q` è un stato dell'automa
> - `w` è una stringa che può essere ottenuta attraverso l’alfabeto dell'automa
>   
>**Configurazione Universale:** $(q_{0}, x)$ dove $q_{0}$ è lo stato iniziale di $M$????

>[!note] Definizione: Passo di computazione 🟢
>
>Definiamo come passo di computazione la relazione binaria definita come:
>
>$$
>(q_{1},aw) \vdash_{M} (q_{2},w) \iff \delta(q_{1},a) = q_{2}
>$$
>
>Dove:
>- $q_{1}, q_{2} \in Q$ 
>- $a \in \Sigma$
>- $w \in \Sigma^{*}$
>
>Queste indica che la configurazione $(q_{1},aw)$ porta alla configurazione $(q_{2},w)$ utilizzando il DFA `M` se e solo se la funzione di accettazione con input $q_{1}$ e $a$  ritorna $q_{2}$.

>[!note] Definizione: Computazione deterministica 🟢
>
>Definiamo una computazione come deterministica se ad ogni passo di computazione segue un’unica configurazione:
>$$
>\forall  (q_{1},aw)\ \  \exists! \ (q_{2},w)\ |\ (q_{1},aw) \vdash_{M} (q_{2},w)
>$$
>
>>*nota:* $\exists!$ significa esiste un unico

>[!note] Definizione: Chiusura riflessiva e transitiva 🟠
>
>Sia $M := (Q,\Sigma,\delta,q_{0},F)$ un DFA. La chiusura riflessiva e transitiva di $\vdash_{M}$ indicata come $\vdash_{M}^{*}$, gode delle seguenti proprietà:
>$$
>\begin{align*}
>\text{Riflessività: }\ \ \ \,  & (q_{1},x) \vdash_{M}^{*} (q_{1}, x)\\
>\text{Transitivita: }\ \ &(q_{1},aby) \vdash_{M} (q_{2},by)\ \wedge \ (q_{2},by) \vdash_{M}(q_{3},y) \implies  (q_{1},aby) \vdash_{M}^{*} (q_{3},y)
>\end{align*}
>$$
>
>E ovviamente vale tutto quello detto precedentemente quindi: $(p_{1}, aw) \vdash_{M}(q_{1},w) \implies (p_{1}, aw) \vdash_{M}^{*}(q_{1},w)$

## Esempio creazione di un Automa

Obbiettivo dato il linguaggio $L = \{  x \in \{ 0,1 \}^{*}\ :\ x=1y,\; \ y \in \{ 0,1 \}^{*} \}$ dobbiamo creare un DFA che lo accetti:

In questo linguaggio le stringhe iniziano tutte con il carattere `1` e poi hanno una sequenza di caratteri `0`,`1`.

Una automa che accetta ogni stringa in `L` è:

![[Pasted image 20250926160552.png|800]]

Notiamo quindi che questo accetta soltanto le stringhe che iniziano con il carattere `1`, infatti se riceve `1` entra nello stato $q1​$ e non esce più, mentre se riceve `0` entra nello stato $q_{2}$​ senza più uscire.

>[!warning] Dimostrazione Correttezza Automa
>
>Adesso dobbiamo dimostrare che questo DFA accetta il linguaggio, quindi più formalmente:
>
>$$
>\text{DFA accett}\ x \iff X \in L
>$$
>
>Iniziamo osservando che se ci troviamo in $q_{1}$​ rimarremo sempre in $q_{1}$​ e stessa cosa anche per $q_{1}$​, formalmente:
>
>$$
>\begin{align*}
>&\delta(q_{1}, u) = q_{1} \forall  u \in \{ 0,1 \}^{*}\\ \\
>&\delta(q_{2}, u) = q_{2} \forall  u \in \{ 0,1 \}^{*}
>\end{align*}
>$$
>  
>Tenendo in mente questo ragionamento iniziamo la dimostrazione per induzione:
>  
>>**Caso Base** $|x| = 0$ quindi $x = \epsilon$
>>- Otteniamo che $\delta^{*}(q_{0},\epsilon) = \delta(q_{0},\epsilon)=q_{0} \not \in F$
>>- Quindi con una stringa vuota rimaniamo sempre in $q_{0}$​ che non è uno stato di accettazione del DFA
>
>>**Passo Induttivo**
>>
>>In questo caso abbiamo quindi $|w| \leq n$ con $n\geq0$, e quindi la funzione di transizione estesa avrà questi risultati possibili:
>>
>>$$
>>\delta^{*}(q_{0}, w) = \begin{cases}
>>q_{0} & \text{se } w = \epsilon \\
>> q_{1}& \text{se } w \text{ inizia con } 1 \\
>> q_{2}& \text{se } w \text{ inizia con } 0
>>\end{cases}
>>$$
>>
>>Adesso prendiamo una stringa $|x| = n+1$ e la pensiamo costruita come $x=au$ con $a\in \{0,1\}$ e $u\in \{0,1\}^{*}$, la funzione di transizione ci restituirà:
>>
>>$$
>>\delta^{*}(q0​,x) = \delta^{*}(q0​,au)=\delta^{*}(\underbrace{\delta(q_{0}​,a)}_{\text{solo 2 soluzioni}}​​,u)
>>$$
>>
>>Le due soluzione del passaggio sono:
>>- $\delta(q_{0},a) = q_{1}$ se $a=1$
>>- $\delta(q_{0},a) = q_{2}$ se $a=0$
>>
>>Ricordando cosa abbiamo detto all’inizio, sappiamo che sia che ci troviamo in $q_{1}$​ o $q_{2}$​ rimarremo sempre li, indipendentemente da come è fatta la stringa $u$.

