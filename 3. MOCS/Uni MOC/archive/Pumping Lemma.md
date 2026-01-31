---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2025-10-10T18:34
updated: 2026-01-31T13:32
---
## Teorema

Il pumping lemma è un teorema che permette di testare la regolarità di un linguaggio. Infatti questo teorema afferma che tutti i linguaggi regolari hanno una proprietà speciale, se riusciamo a dimostrare che un linguaggio non ha questa proprietà allora non sarà regolare.

Come vedremo questa proprietà afferma che tutte le stringhe nell linguaggio possono essere "replicate" all'infinito, se raggiungono una determinata lunghezza "speciale" chiamata *lunghezza di pumping*.

>[!note] Pumping Lemma
>
>Se $L$ è un linguaggio regolare $L \in \text{REG}$, allora esiste un numero $p \in \mathbb{N}$ detto ***lunghezza di pumping*** tale che $\forall w \in L$ e $|w|\geq p$ abbiamo che:
>
>La stringa $w$ può essere divisa in tre parti ($W = zyx$) soddisfacenti le seguenti condizioni:
>- $\forall i \geq 0\ \ xy^{i}z \in L\ \ \ \ \ \big( \text{ossia è possibile concatenare } y \text{ per } i \text{ volte rimanendo in } L \big)$
>- $|y| > 0 \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \big( \text{ossia }  y \not = \epsilon \big)$
>- $|xy| \leq p \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \big( \text{ossia } y \text{deve trovarsi nei primi } p \text{ simboli di } w \big)$

>[!warning] Dimostrazione
>
>Dato $L \in \text{REG}$, sia $D := \big(Q,\Sigma,\delta,q_{0}, F\big)$ il DFA tale che $L = L(D)$
>
>Consideriamo quindi $p := |Q|$ e la data la stringa $w := w_{1}\dots w_{n} \in L$ dove:
>- $w_{1},\dots,w_{n} \in \Sigma$
>- $n \geq p$
>
>Consideriamo la sequenza di stati $r_{1}, \dots, r_{n+1}$ tramite cui $w$ viene accetta da $D$:
>
>$$
>\forall k \in \big[1,n\big]\ \ \delta(R_{k},\, w_{k}) = r_{k+1}
>$$
>
>Notiamo quindi che il numero di stati attraversati sia $n+1$ (ovvero $|r_{1},\dots ,r_{n+1} | = n+1$), inoltre:
>- in quanto $n \geq p$ ne segue che $n+1 \geq p+1$.
>  
>Tuttavia, poiché $p:= |Q|$ e $n+1 \geq p+1$ ne segue che:
>- $\exists i,j\ \mid \ 1\leq i < j\leq p+1 \wedge r_{i} = r_{j}$
>- ovvero che tra i primi $p+1$ stati della sequenza vi sia almeno uno stato ripetuto
>  
>A questo punto, consideriamo le seguenti sotto stringhe di $w$:
>- $x = w_{1}\dots w_{i-1}$, tramite cui si ha che $\delta^{*}(r_{1},x) = r_{i}$
>- $y = w_{1}\dots w_{j-1}$, tramite cui si ha che $\delta^{*}(r_{i},y) = r_{j} = r_{i}$
>- $z = w_{j}\dots w_{n}$, tramite cui si ha che $\delta^{*}(r_{j},z) = r_{n+1}$
>  
>Poiché $\delta^{*}(r_{i},y) = r_{i}$, ossia $y$ porta sempre $r_{i}$ in se stesso, ne segue automaticamente che:
>
>




