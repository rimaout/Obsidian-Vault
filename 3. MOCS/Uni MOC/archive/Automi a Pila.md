---
type: Uni Note
class:
  - "[[Automi (class)]]"
academic year: 2024/2025
related:
completed: false
created: 2025-10-23T17:18
updated: 2025-10-24T17:20
---
## Introduzione

Introduciamo un nuovo tipo di modello computazionale chiamato **automa a pila** (pushdown automata). Questi automi sono come gli automi finiti non deterministici ma hanno una componente in più chiamata pila (stack).

Dimostreremo che la pila consente di creare automi che sono computazionali equivalenti a grammatiche context-free, ovvero automi che riconoscono linguaggi context-free.

Una pila è una struttura dati *last in, last out* dove tutte le operazioni sono effettuate dalla cima, in particolare ci sono:
- `push` che inserisce un simbolo in cima alla pila
- `pop` che elimina l'elemento in cima alla pila

## Definizione PDA

La definizione di un automa a pila è simile alla definizione di un automa finito $(Q, \Sigma, \delta,q_{0},F)$ ma a cui viene aggiunta la pila.

La pila ha un suo alfabeto ($\Gamma$) che può essere diverso dall'alfabeto dell'automa.

In particolare la funzione di transizione $\delta$ è diverse rispetto ad un automa finite.

Il **dominio** di $\delta$ è $Q \times \Sigma_{\epsilon} \times \Gamma_{\epsilon}$, quindi il futuro stati dipende da:
- lo stato corrente
- il simbolo in input letto
- il simbolo in cima alla pila

>L'uno o l'altro simbolo può essere $\epsilon$, il che determina che la macchina si muova senza leggere un simbolo di input o senza leggere un simbolo dalla pila.

Il condominio di $\delta$  è $\mathcal{P}(Q \times \Gamma_{\epsilon})$, quindi il risultato è descritto da:
- lo stato in cui ha portato la transizione
- il carattere che è stato aggiunto in cima alla pila

>Il simbolo aggiunto alla pila può anche essere $\epsilon$, significando che non è stato aggiunto nessun simbolo.

Quindi la funzione di transizione assume la forma:

$$
\delta: Q \times  \Sigma_{\epsilon} \times \Gamma_{\epsilon} \to  \mathcal{P}(Q \times \Gamma_{\epsilon})
$$

>[!note] Definizione: Pushdown Automaton (PDA)
>
>Un automa a pila è una tupla $\big(Q, \Sigma, \Gamma, \delta, q_{0}, F \big)$ dove:
>- $Q$ è l'insieme finito di degli *stati dell'automa*
>- $\Sigma$ è l'*alfabeto dell'automa*
>- $\Gamma$ è l'*alfabeto dello stack* dell'automa
>- $q_{0} \in Q$ è lo *stato iniziale* dell'automa
>- $F \subseteq Q$ è l'insieme degli *stati accettanti* dell'automa
>
>$\delta:Q \times \Sigma_{\epsilon} \times \Gamma_{\epsilon} \to \mathcal{P}(Q \times \Gamma_{\epsilon})$ è la funzione di transizione dell'automa, dove se $(q,c) \in \delta(p,a,b)$ si ha che:
>- Viene letto il simbolo `a` dalla stringa in input e se il simbolo `b` è in cima allo stack allora l’automa passa dallo stato `p` allo stato `q` e il simbolo `b` viene sostituito dal simbolo `c`
>- L’etichetta della transizione da `p` a `q` viene indicata come $a;\, b \to c$
>  
>>***nota:*** $\Sigma_{\epsilon} = \Sigma \cup \{ \epsilon \}$

>[!warning] Approfondimento (operazioni)
>
>Dato $(q, c) \in \delta(p, a, b)$ dove $\delta$ è la funzione di transizione di un PDA, si ha che:
>- Se $b, c = \epsilon$ (dunque $a; \epsilon \to \epsilon$) allora l’automa leggerà `a` dalla stringa e passerà direttamente dallo stato `p` allo stato `q`, senza modificare lo stack
>- Se $b = \epsilon$ e $c \not = \epsilon$ (dunque $a; \epsilon \to c$) allora l’automa leggerà `a` dalla stringa, passerà direttamente dallo stato `p` allo stato `q` e in cima allo stack viene aggiunto il simbolo `c` (**push**)
>- Se $n \not = \epsilon$ e $c = \epsilon$ (dunque $a; b \to \epsilon$) allora l’automa leggerà `a` e se in cima allo stack vi è `b`, l’automa passerà dallo stato `p` allo stato `q` e rimuoverà `b` dalla cima dello stack (**pop**)

>[!example] Esempio
>
>Consideriamo il seguente PDA:
>
>![[Pasted image 20251024171301.png|500]]
>
>Data la stringa `aab`, uno dei possibili rami di computazione del PDA procede nel seguente ordine:
>1. Viene letta la prima `a` e viene inserita la prima `c` in cima allo stack, rimanendo nello stato $q_{1}$
>2. Viene letta la seconda `a` e viene inserita la seconda `c` in cima allo stack, rimanendo nello stato $q_{1}$
>3. Viene letta la `b`, e quindi si passa allo stato $q_{2}$
>4. Viene "letta" la prima $\epsilon$, rimuovendo la seconda `c` dallo stack (poiché essa è in cima), rimanendo nello stato $q_{2}$
>5. Viene "letta" la seconda $\epsilon$, rimuovendo la prima `c` dallo stack (poiché essa è in cima), rimanendo nello stato $q_{3}$
>6. Sia la stringa che lo stack sono vuoti, dunque la computazione termina necessariamente poiché non vi sono transizioni percorribili
>
>Notiamo in particolare che, in tal caso, la stringa verrebbe accettata anche se la computazione si fermasse al terzo passo
>
>Difatti, lo stack non deve necessariamente esser vuoto affinché la stringa possa essere accettata

## Stringa accettata da un PDA

