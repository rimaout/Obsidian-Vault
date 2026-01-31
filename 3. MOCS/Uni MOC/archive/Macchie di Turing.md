---
type: Uni Note
class:
  - "[[Automi (class)]]"
academic year: 2024/2025
related:
completed: false
created: 2025-11-07T08:20
updated: 2026-01-31T13:32
---
## Introduzione

Nel 1936, il pioniere dell’informatica Alan Turing sviluppò un modello di calcolo simile ad un automa a stati finiti ma dotato di una **memoria illimitata** e senza alcuna restrizione.

Sebbene essa richieda una grande mole di tempo, la *macchina di Turing* è in grado di elaborare tutto ciò che un **reale computer** è in grado di elaborare. Per tanto, essa costituisce un perfetto modello astratto di un reale computer, implicando che ogni problema per essa **irrisolvibile** lo sarà anche per un computer.

>[!note] Struttura Macchina
>
>Il modello di Turing utilizza un **nastro infinito** (*solo a destra*) come memoria illimitata ed è dotata di una testina di lettura-scrittura. Il nastro è formato da celle, le quali, inizialmente, contengono solo una stringa data in input (tutte le altre celle sono vuote).
>
>Inoltre, il nastro viene continuamente spostato a sinistra e destra, in modo che la testina possa leggere o scrivere sulle varie celle. La macchina continua la sua computazione finché essa non raggiungerà lo stato di *accettazione* o lo stato di *rifiuto* della stringa in input.
>
>>***Nota:*** Se la macchina non è in grado di raggiungere nessuno dei due stati, essa rimarrà in un loop infinito, non terminando mai l’esecuzione.

>[!example] Esempio Informale
>
>Ad esempio, consideriamo il linguaggio $L = \{ w\#w \mid w \in \{ 0,1 \}^{*} \}$. Descriviamo in modo informale una macchina di Turing `M` in grado di accettare le stringhe di `L`.
>
>M = Data la stringa `s` in input:
> 1. Muoviti a zig-zag lungo il nastro tra tutte le posizioni corrispondenti su entrambi i lati del simbolo `#`. Se i due simboli combaciano, cancella entrambi sovrascrivendoli con una `x`. Se i due simboli non combaciano o se non viene mai trovato il simbolo `#`, rifiuta la stringa.
> 2. Quando tutti i simboli a sinistra del simbolo `#` sono stati cancellati, controlla se a destra del simbolo `#` vi sono simboli diversi da `x`. Se vi sono, rifiuta la stringa, altrimenti accettala.
>
>>***Nota:*** il simbolo $\textvisiblespace$ indica una cella vuota.

## Definizione di TM

Una **Turing Machine (TM)** è una tupla $\big(Q, \Sigma, \Gamma, \delta, q_{\text{start}}, q_{\text{accept}}, q_{\text{reject}}\big)$ dove:
- $Q$ è l'*insieme finito degli stati* della macchina
- $\Sigma$ è l'*alfabeto della macchina*, dove $\textvisiblespace \in \Sigma$
- $q_{\text{start}}\in Q$ è lo *stato iniziale* dell'automa
- $q_{\text{accept}}\in Q$ è lo *stato accettante* dell'automa
- $q_{\text{reject}}\in Q$ è lo *stato rifiutante* dell'automa, dove $q_{\text{accept}} \neq q_{\text{reject}}$

$\delta$ è la **funzione di transizione della macchina** definita come :

$$
\delta: Q - \{ q_{\text{accept}}, q_{reject} \}  \times \Gamma \to Q \times \Gamma \times \{ L, R \}
$$
Dove se $\delta(p,a) = (q,b,X)$ si ha che:
- Viene letto il simbolo `a` dal nastro, sostituendolo con `b` e la macchina passa dallo stato `p` allo stato `q`. Inoltre, il nastro viene spostato a sinistra se $X = L$ e a destra se $X = R$.
-  L’etichetta della transizione da `p` a `q` viene indicata come $a \to b; X$

>[!warning] Note
>
>Una macchina di Turing $M = \big(Q, \Sigma, \Gamma, \delta, q_{\text{start}}, q_{\text{accept}}, q_{\text{reject}}\big)$ computa nel seguente modo. 
>
>Inizialmente M riceve il suo input $w = w_{1},w_{2},\dots,w_{n} \in \Sigma^{*}$ sulle `n` celle più a sinistra del nastro, mentre il resto del nastro è vuoto (cioè, contiene tutti simboli blank). 
>
>La testina parte dalla posizione più a sinistra del nastro. Si noti che $\Sigma$ non contiene il simbolo blank, in tal modo il primo simbolo blank che compare sul nastro segna la fine dell'input.
>
>Quando `M` inizia la computazione, questa procede secondo le regole descritte dalla funzione di transizione. Se `M` tenta di spostare la testina a sinistra quando si trova all'estremità sinistra del nastro, allora la testina rimane nello stesso posto per quella mossa, anche se la funzione di transizione indica `L`. La computazione prosegue fin quando la macchina raggiunge lo stato di accettazione oppure di rifiuto, a tal punto si ferma. Se nessuno dei due stati viene raggiunto, `M` va avanti per sempre.

## Configurazione, Passo di Computazione e Stringa Accetta

>[!note] Configurazione
>
>Sia $M = \big(Q, \Sigma, \Gamma, \delta, q_{\text{start}}, q_{\text{accept}}, q_{\text{reject}}\big)$ una TM. Definiamo ka stringa `uqav` come *configurazione* di $M$, dove:
>- $q \in Q$ è lo stato attuale della macchina
>- $a \in \Gamma$ è il simbolo del nastro su cui si trova attualmente la testina della macchina
>- $u \in \Gamma^{*}$ è composta dai simboli precedenti ad $a$ sul nastro 
>- $v \in \Gamma^{*}$ è composta dai simboli successivi ad $a$ sul nastro

>[!note] Passo di Computazione
>
>Si dice che la configurazione `c1` produce la configurazione `c2` se la macchina di Turing può passare da `c1` a `c2` in un unico passo.
>
>**Formalmente:** Dati $a,b,c \in \Gamma$ (simboli nastro), $u,v \in \Gamma^{*}$ (stringhe nastro), $q_{i},q_{j} \in Q$ (stati macchina), allora diciamo che:
>
>$$
>\begin{align*}
>&uaq_{i}bv\ \ \ \text{ produce } \ \ \ uq_{j}acv
>\ \ \ \ (\text{se } \delta(q_{i},b) = (q_{j}, c, L))\\ \\
>&uaq_{i}bv\ \ \ \text{ produce } \ \ \ uacq_{j}v
>\ \ \ \ (\text{se } \delta(q_{i},b) = (q_{j}, c, R))
>\end{align*}
>$$
>
>---
>**Spiegazione** della prima computazione:
>
>La configurazione sinistra ($uaq_{i}bv$) composta da:
>- `b` è il simbolo su cui si trova la testina
>- `u` sono i simboli (stringa) che si trovano subito dopo la testina
>- `a` è il simbolo subito precedente alla testina
>- `u` sono i simboli (stringa) subito precedenti ad `a` (e quindi anche precedenti alla testina)
>- $q_{i}$ è lo stato attuale dell macchina
>
>Ora se applichiamo $\delta(q_{i},b) = (q_{j}, c, L)$ quindi:
>- la macchina passa dallo stato $q_{i}$ allo stato $q_{j}$
>- il simbolo `b` (su cui si trova la testina) viene rimpiazzato dal simbolo `c`
>- la testina viene spostata a sinistra, quindi ora punta al carattere `a`.

>[!note] Stinga accettata
>
>$M = \big(Q, \Sigma, \Gamma, \delta, q_{\text{start}}, q_{\text{accept}}, q_{\text{reject}}\big)$ una TM. La stinga $w \in \Sigma^{*}$ si dice accettata da `M` se esiste una sequenza di configurazioni $c_{1}, c_{2}, \dots, c_{k}$ tale che:
>- $c_{1} = q_{\text{start}}w$
>- $\forall i \in [1, k-1]\ \ c_{1}\ \ \text{produce}\ \ c_{i+1}$
>- $q_{\text{accept}} \in c_{k}$
>  
>>[!example] Esempio
>>Il linguaggio $L = \{ 01^{n}0 \mid n \in \mathbb{N}\}$ è riconosciuto dalla seguente TM:
>>
>>![[Pasted image 20251119104414.png|900]]
>>
>> Difatti, durante la lettura della stringa 01110, la macchina assume le seguenti configurazioni:
>> 
>>$$
>>\begin{array}{ccccccc}
>>x & q_{1} & 0 & 1 & 1 & 1 & 0 \\
>>x & q_{2} & 1 & 1 & 1 & 0 &   \\
>>x & y & q_{3} & 1 & 1 & 0 &   \\
>>x & y & y & q_{4} & 1 & 0 &   \\
>>x & y & y & y & q_{5} & 0 &   \\
>>x & y & y & y & x & q_{6} &   \\
>>\end{array}
>>$$


