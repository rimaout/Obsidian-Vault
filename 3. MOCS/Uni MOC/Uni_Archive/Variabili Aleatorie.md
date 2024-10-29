---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2024-10-29T15:31
updated: 2024-10-29T16:46
---
>[!abstract] Index
>1. 

>[!abstract] Related
>- 

>[!danger] TLDR

---
## Variabili Aleatorie (Reali)

>[!note] Definizione
>Dato uno spazio di probabilità $(S,P)$, una variabile aleatoria è una funzione $X$ tale che $X:S \to \mathbb{R}$.
>
>Ovvero una funzione che mappa elementi dello spazio campionario $S$ a numeri reali.

>[!example]- Esempio 1
>Lancio una moneta 2 volte e definiamo $X$ come $X := \#\text{numero di volte in cui esce testa}$
>
>Lo spazio campionario è $S = \{ (T,T), (T,C), (C,T), (C,C) \}$ - (esiti equiprobabili)
>
>- $X((T,T)) =2$ 
>- $X((T,C))=1$
>- $X((C,T)) = 1$ 
>- $X((C,C)) =0$

^08d948

>[!example]- Esempio 2
>Lancio due volte un dato, chiamiamo $X$ la somma dei risultati $X:= \#\text{somma numeri usciti}$
>
>Lo spazio campionario è $S= \{ (a,b) :a,b \in \{ 1,2,3,4,5,6 \}\}$ - (esiti equiprobabili)
>
>- $X((a,b)) = a+b\ \ \ \ es:\ X((1,5)) = 6$

^583bec

---
## Variabili Aleatorie Discrete

Una variabile aleatoria $X$ è detta **discreta** se i valori che può assumere $\{ x_{i} \}_{i\in I}$ formano un  *insieme finito o infinito numerabile*.

>[!example]- Esempio
>Le variabili aleatorie degli esempi precedenti [[#^08d948|1]] e [[#^583bec|2]] sono discrete, infatti:
>- nel  [[#^08d948|primo esempio]] la variabile aleatoria $X$ può assumere soltanto valori appetenti ad $\{ 0,1,2 \}$
>- nel  [[#^583bec|secondo esempio]] esempio la variabile aleatoria $X$ può assumere soltanto valori appetenti ad $\{ 2,3, \dots, 12 \}$
>
>E ovviamente sono tutti e due insiemi finiti.

### Densità di Probabilità Discreta

>[!note]  Definizione
>La densità di probabilità discreta è una funzione che descrive la probabilità di ciascun valore possibile di una variabile aleatoria discreta.
>
>**Matematicamente:**
>Data una variabile aleatoria discreta $X$, che assume valori $\{ x_{i} \}_{i \in I}$ definiamo la densità di probabilità diserta di $X$ come la funzione:
>
>$$
>Px:\{ x_{i} \}_{i \in I} \to [0,1],\  P_{X}(x_{i}):=P(X=x_{i})
>$$
>
>Ovvero la funzione che preso un valore che può assumere la variabile aleatoria ne ritorna la sua probbailità (ovvero un valore compreso tra 0 e 1)
>
>**Notazione:**
>Con $P_{X} (x_{i})$ indichiamo la probabilità che la variabile aleatoria $X$ assuma il valore $x_{i}$.

>[!example]- Esempio
>
>Nel caso del [[#^08d948|primo esempio]] visto in precedenza dove abbiamo che:
>- La variabile aleatoria $X$ e definita come $X := \#\text{numero di volte in cui esce testa}$
>- L'insieme dei possibili risultati che può assumere $X$ è $\{ 0,1,2 \}$
>  
>La funzione di probabilità discreta è:
>$$
>P_{X}(a) = \begin{cases}
>1/4 & \text{se } a = 0 \\
>1/2 & \text{se } a = 1 \\
>1/4 & \text{se } a = 2 \\
>0 & \text{altrimenti}
>\end{cases}
>$$
>
>Dove:
>$$
>\begin{align*}
>&P_{X} = \{ 0,1,2 \} \to  [0,1]\\
>&P_{X}(a) = P(X=a)\\
>&P_{X}(0) = P(X=0) = 1/4, P_{X}(1) = P(X=1) = 2 / 4, P_{X}(2) = P(X=2) = 1 / 4
>\end{align*}
>$$
>
>>[!warning] Osservazione
>>Quando scriviamo $P(X=1)$ intendiamo che $P(\{ s \in S: X(s) =1  \}) = P(\{ (C,T), (T,C) \}) = \frac{2}{4}$

---
## Valore Atteso

>[!note] Definizione
>Il valore atteso di una variabile aleatoria rappresenta il valore medio che ci si aspetta di ottenere se si ripetesse un esperimento aleatorio un numero infinito di volte
>
>**Matematicamente:**
>Data una variabile aleatoria $X$ che assume valori $\{ x_{i} \}_{i \in I}$ definiamo il valore atteso $X$  come:
>
>$$
>E\big[X\big] = \sum_{i \in I} x_{i} P(X=x_{i}) = \sum_{i \in I} x_{i} P_{X} (x_{i})
>$$
>
>>Dove $E\big[X\big]$ indica _expected value of X_.

>[!example]- Esempio 1
>Lanciamo 2 due volte una moneta e definiamo una variabile aleatoria $X = \#\text{ esce testa}$
>
>I valori possibili di $X$ sono 0, 1 e 2; la probabilità di ciascun valore è la seguente:
>* $P(X=0) = 1/4$ (esce croce due volte)
>* $P(X=1) = 1/2$ (esce testa una volta e croce una volta)
>* $P(X=2) = 1/4$ (esce testa due volte)
>
>Il valore atteso di $X$ è:
>
>$$E\big[X\big] = 0 \cdot P(X=0) + 1 \cdot P(X=1) + 2 \cdot P(X=2)$$
>$$E\big[X\big] = 0 \cdot (1/4) + 1 \cdot (1/2) + 2 \cdot (1/4)$$
>$$E\big[X\big] = 0 + 1/2 + 1/2$$
>$$E\big[X\big] = 1$$
>
>Quindi, il valore atteso di $X$ è 1. Ciò significa che se si lancia la moneta due volte molte volte, ci si aspetta di ottenere in media 1 testa.

>[!example]- Esempio 2
>Data un’urna con 3N e 2B. Estraggo due palline senza rimpiazzo, sia $X := \# \text{palline nere estreatte}$, calcolare calcolare $E[X]$.
>
>Abbiamo $X=\{0,1,2\}$
>
>- $P(X=0)=5 \cdot 42 \cdot 1 = 202​$
>- $P(X=1)=5 \cdot 43 \cdot2 ​+ 5 \cdot 42 \cdot 3​ = 2012​$
>- $P(X=2) = 5 \cdot 43 \cdot 2​ = 206​$
>
>Allora: $E[X]=0\cdot 202​+1\cdot 2012​+2 \cdot 206​=56​$

>[!example]- Esempio 3
>Supponiamo di avere una lotteria in cui si possono vincere 0, 10 o 100 euro. Le probabilità di vincere ciascun importo sono le seguenti:
>
>* $P(X=0) = 0,9$ (non si vince nulla)
>* $P(X=10) = 0,09$ (si vince 10 euro)
>* $P(X=100) = 0,01$ (si vince 100 euro)
>
>Il valore atteso di $X$ è:
>$$E\big[X\big] = 0 \cdot 0,9 + 10 \cdot 0,09 + 100 \cdot 0,01$$
>$$E\big[X\big] = 0 + 0,9 + 1$$
>$$E\big[X\big] = 1,9$$
>
>Quindi, il valore atteso di $X$ è 1,9 euro. Ciò significa che se si giocasse alla lotteria molte volte, ci si aspetta di vincere in media 1,9 euro.

---
## Funzione di Distribuzione (o Ripartizione)

>[!note] Definizione
>La funzione di distribuzione (o ripartizione) è una funzione matematica che descrive la probabilità che una variabile aleatoria assuma valori inferiori o uguali a un certo valore.
>
>$F_{X}​\mathbb{R}\to [0,1] \text{ con } F_{x}​(a) = P(X\leq a)\  \forall a \in \mathbb{R}$
