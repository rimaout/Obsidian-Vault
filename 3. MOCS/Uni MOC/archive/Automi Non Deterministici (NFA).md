---
type: Uni Note
class:
  - "[[Automi (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-10-01T17:46
updated: 2026-09-25T16:00
---
>[!note] Definizione: Alfabeto epsilon
>
>Dato un alfabeto $\Sigma$, definiamo $\Sigma_{\epsilon} = \Sigma \cup  \{ \epsilon \}$ come alfabeto epsilon di $\Sigma$.

>[!note] Definizione: Non-deterministic Finite Automaton (NFA)
>
>Un Non-deterministic Finite Automaton (NFA) (o Automa Non-deterministico a Stati Finiti) è una quintupla $(Q, \Sigma, \delta, q_{0}, F )$ dove:
>
>- $Q$ è l’insieme finito degli stati dell’automa
>- $\Sigma$ è l’alfabeto dell’automa
>- $\delta : Q \times \Sigma_{\epsilon} \to \mathcal{P}(Q)$ è la funzione di transizione degli stati dell’automa
>- $q_{0} \in Q$ è lo stato iniziale dell’automa
>- $F \subseteq Q$ è l’insieme degli stati accettanti dell’automa
>
>Nota: $\mathcal{P}(Q)$ è l’insieme delle parti di $Q$, ossia l’insieme contenente tutti i suoi sottoinsiemi possibili.
>
>>[!example]- Esempio di NFA
>>
>>Consideriamo il seguente NFA:
>>![[Pasted image 20251001182950.png|500]]
>>
>>dove:
>>– $Q = \{q_{1}, q_{2}, q_{3}\}$ è l’insieme degli stati dell’automa
>>– $\Sigma = \{a, b\}$ è l’alfabeto dell’automa
>>– $\delta : Q \times \Sigma^{\epsilon} \to \mathcal{P} (Q)$ definita come:
>>
>>![[Pasted image 20251001183030.png|300]]
>>
>>Dove:
>>- $q_{1}$ è lo stato iniziale dell’automa
>>- $F = \{q1\}$ è l’insieme degli stati accettanti

>[!warning] Osservazione: Computazione in un NFA
>Sia $N := (Q, \Sigma, \delta, q_{0}, F )$ un NFA. Data una stringa $w \in \Sigma^{*}$ in ingresso, la computazione viene eseguita nel seguente modo:
>- Tutte le volte che uno stato potrebbe avere più transizioni per diversi simboli dell’alfabeto, l’automa $N$ si *duplica in più copie*, ognuna delle quali segue il suo corso. Si vengono così a creare più **rami di computazione** indipendenti che sono eseguiti in **parallelo**.
>- Se il prossimo simbolo della stringa da computare non si trova su nessuna delle transizioni uscenti dello stato attuale di un ramo di computazione, l’intero ramo termina la sua computazione (terminazione incorretta).
>- Se almeno una delle copie di $N$ termina correttamente su uno stato di accettazione, l’automa accetta la stringa di partenza.
>- Quando a seguito di una computazione ci si ritrova in uno stato che possiede un $\epsilon$-arco in uscita, la macchina si duplica in più copie: quelle che seguono gli $\epsilon$-archi e quella che rimane nello stato raggiunto.

>[!example] Esempio: Albero computazione parallela
>
>Consideriamo il seguente NFA:
>
>![[Pasted image 20251003121749.png|700]]
>
>Supponiamo che venga computata la stringa `w = 1010:`
> 
>![[Pasted image 20251003122132.png|600]]
>
>Dato che esiste un ramo che termina su uno stato di accettazione (`q3`), l’NFA descritto accetta la stringa `w = 1010`.
>
>>[!warning] Ossevazioni
>>- Ogni livello rappresenta un numero di caratteri nella stringa
>>- Quando si traversa un $\epsilon\text{-arco}$ non viene "utilizzato" nessun carattere.

>[!note] Proposizione: Stringa accettata in un NFA
>
>Sia $N := (Q, \Sigma, \delta, q_{0}, F)$ un NFA. Data una stringa $w:= a_{0},a_{1},\dots a_{k}$, dove $a_{0},\dots,a_{k} \in \Sigma$, diciamo che $w$ è accettata da $N$ se esiste una sequenza di stati $r_{0}, r_{1}, \dots, r_{k+1} \in Q$ tali che:
>1. $r_{0} = q_{0}$
>2. $\forall i \in [0,k]\ \ r_{i+1} \in \delta(r_{i}, a_{i})$
>3. $r_{k+1} \in F$
>   
>**Spiegazione:**
>- La condizione 1 dice che la macchina inizia dallo stato iniziale.
>- La condizione 2 dice che lo stato $r_{i}+1$ è uno dei possibili stati successivi di $r_{i}$ quando si sta leggendo il carattere $a_{i}$.
>- Le condizione 3 dice che la macchina accetta il suo input se l'ultimo stato è uno stato accettante.

