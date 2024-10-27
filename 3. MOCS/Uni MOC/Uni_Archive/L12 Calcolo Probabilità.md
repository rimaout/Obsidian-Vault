---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2024-10-25T12:05
updated: 2024-10-26T15:15
---
## Variabili Aleatorie (reali)

>[!note] Definition
>Dato uno spazio di probabilità (S,P), una variabile aleatoria è una funzione $S:S \to \mathbb{R}$.
>

>[!example] Esempio
>Lancio una moneta 2 volte. definisco $X$ come $X:= \#\text{volte in cui esce testa}$
>
>Allora $X$ è una variabile aleatoria
>
>$$
>S = \{ (T,T), (T,C), (C,T), (C,C) \}
>$$
>
>- $X(T,T) =2, Z(T,C)=1, X(C,T) =1 dljshdzjlkzh lxzjk$

>[!example] Esempio 
>Lancio due volte un dato, chiamiamo $X$ la somma dei risultati $X:= \#\text{somma numeri usciti}$
>
>>*oss* $X$ è variabile aleatoria
>
>$$
S= \{ (a,b) :a,b \in \{ 1,2,3,4,5,6 \}\} \text{ esiti equiprobabili}
>$$
>
>$X((a,b)) = a+b\ \ \ \ es:\ X((1,5)) = 6$

>[!note] Variabile Aleatoria Discreta
>
>una variabile aleatoria $X$ è detta discreta se i valori che può assumere $\{ x_{i} \}_{i\in T}$ formano un insieme numerabile (finito o infinito)

>[!note] 
>Data $X$ variabile aleatoria discreta, la densità di probabilità diserta di $X$ è la funzione:
>
>$$
>Px:\{ x_{i} \}_{i \in I} \to [0,1], P_{X}(x_{i}):=P(X=x_{i})
>$$

>[!example] Example
>- $S = \{ s_{1},s_{2} \}$
>- $X(s_{1})=a_{1}, X(s_{2})=a_{2}$
>  allora:
>$$
>P_{X} = \{ a_{1},a_{2} \} \to  [0,1]
>$$
>- $P_{a_{1}} = P(X=a_{1})$
>- $P_{a_{2}} = P(X=a_{2})$

>[!example] Example:
>2 lanci di una moneta ed $X:= \text{ è il numero delle teste uscite}$
>
>oss:
>- $X((T,T)) =2$
>- $X((C,T)) =1$
>- $X((T,C)) =1$
>- $X((C,C)) =0$
>
>$$
>\begin{align*}
>&P_{X} = \{ 0,1,2 \} \to  [0,1]\\
>&P_{X}(a) = P(X=a)\\
>P_{X}(0) = P(X=0) = \frac{1}{4}, P_{X}(1) = P(X=1) \frac{2}{4}, P_{X}(2) = P(X=2) \frac{1}{4}
>\end{align*}
>$$
>
>>**oss:**
>>Quando scriviamo $P(X=1)$ intendiamo:
>>$$
>>P(\{ s \in S: X(s) =1  \}) = P(\{ (C,T), /T,C \}) = \frac{2}{4}
>>$$

>La densotà si èrobabilità discreta $P_{X}$ a vpòte si definisce anceh come $P_{X}: \mathbb{R} \to [0,1]$ con $P_{X}(a) = P(X=a)$. >Notiamo che in tal caso $P_{X}(a) = 0$ se $a \not \in \{ x_{i} \}_{i \in I}$
>
>oss: $x_{i}$ valori assunti dalla variabile aleatoria

>[!example] Example
>Lancio il dado due volte $X:= \text{somma dei valori usciti}$
>- $S = et(a,b): a,b \in \{ 1,2,3,4,5,6 \}$ esiti equiprobabili
>  
>  $$
>X(a,b) = a,+b
>$$
>
>$X$ è variabile aleatoria discreta e assume i valori $\{ 2,3,\dots,12 \}$
>- $P_{X}: \{ 2,3,\dots,12 \}$
>- $P_{X}^{\ \ (2)} = P(X=2)=P(\{ (1,1) \}) = \frac{1}{36}$
>- $P_{X}^{\ \ (3)} = P(X=3)=P(\{ (1,2), (2,1) \}) = \frac{2}{36}$
>
>In generale $P_{X}^{\ \ (k)}$ **aggiungi qui formula chiusa per 

>[!warning] Rappresentazione con Istogramma
>
>Possiamo rappresentare la densità di probabilità discreta con un istogramma
>

>[!note] Definition
>Data una vatriabile aleatoria $X$ che assume valori $\{ x_{i} \}_{i \in I}$ definiamo il valore atteso $X$  come:
>
>$$
>E\big[X\big] = \sum_{i=I} x_{i} P(X=x_{i}) = \sum_{i \in I} x_{i} \cdot _{X} (x_{i})
>$$
>
>>**oss:** usiamo la e perche in inglese valore atteso si scrive Expected value

>[!example] Example
>2 lanci di moneta, $X = \text{ esce testa}$
>
>$$
>\begin{align*}
>E[X] &= 0 \cdot  P(X=0) + \cdot  P(X=1) + 2 \cdot  P(X=2)
>& = 0 \cdot  \frac{1}{4} + 2 \cdot \frac{1}{4 = \frac{4}{4}} =1
>\end{align*}
>$$