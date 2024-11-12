---
type: Uni Note
class:
  - "[[Calcolo delle Probabilità (class)]]"
academic year: 2024/2025
related: 
completed: false
created: 2024-10-29T15:31
updated: 2024-11-12T15:19
---

>[!abstract] Related
>- 

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

Una variabile aleatoria $X$ è detta **discreta** se i valori che può assumere $\{ x_{i} \}_{i\in I}$ formano un *insieme finito o infinito numerabile*.

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
>
>>[!example]- Esempio 1
>>Lanciamo 2 due volte una moneta e definiamo una variabile aleatoria $X = \#\text{ esce testa}$
>>
>>I valori possibili di $X$ sono 0, 1 e 2; la probabilità di ciascun valore è la seguente:
>>* $P(X=0) = 1/4$ (esce croce due volte)
>>* $P(X=1) = 1/2$ (esce testa una volta e croce una volta)
>>* $P(X=2) = 1/4$ (esce testa due volte)
>>
>>Il valore atteso di $X$ è:
>>
>>$$E\big[X\big] = 0 \cdot P(X=0) + 1 \cdot P(X=1) + 2 \cdot P(X=2)$$
>>$$E\big[X\big] = 0 \cdot (1/4) + 1 \cdot (1/2) + 2 \cdot (1/4)$$
>>$$E\big[X\big] = 0 + 1/2 + 1/2$$
>>$$E\big[X\big] = 1$$
>>
>>Quindi, il valore atteso di $X$ è 1. Ciò significa che se si lancia la moneta due volte molte volte, ci si aspetta di ottenere in media 1 testa.
>
>>[!example]- Esempio 2
>>Data un’urna con 3N e 2B. Estraggo due palline senza rimpiazzo, sia $X := \# \text{palline nere estreatte}$, calcolare calcolare $E[X]$.
>>
>>Abbiamo $X=\{0,1,2\}$
>>
>>- $P(X=0)=5 \cdot 42 \cdot 1 = 202​$
>>- $P(X=1)=5 \cdot 43 \cdot2 ​+ 5 \cdot 42 \cdot 3​ = 2012​$
>>- $P(X=2) = 5 \cdot 43 \cdot 2​ = 206​$
>>
>>Allora: $E[X]=0\cdot 202​+1\cdot 2012​+2 \cdot 206​=56​$
>
>>[!example]- Esempio 3
>>Supponiamo di avere una lotteria in cui si possono vincere 0, 10 o 100 euro. Le probabilità di vincere ciascun importo sono le seguenti:
>>
>>* $P(X=0) = 0,9$ (non si vince nulla)
>>* $P(X=10) = 0,09$ (si vince 10 euro)
>>* $P(X=100) = 0,01$ (si vince 100 euro)
>>
>>Il valore atteso di $X$ è:
>>$$E\big[X\big] = 0 \cdot 0,9 + 10 \cdot 0,09 + 100 \cdot 0,01$$
>>$$E\big[X\big] = 0 + 0,9 + 1$$
>>$$E\big[X\big] = 1,9$$
>>
>>Quindi, il valore atteso di $X$ è 1,9 euro. Ciò significa che se si giocasse alla lotteria molte volte, ci si aspetta di vincere in media 1,9 euro.

>[!danger] Proposizione
>Sia $X$ una variabile aleatoria discreta e $a,b \in \mathbb{R}$, allora:
>
>$$
>E[aX+b] = aE[X] + b
>$$
>
>>[!warning]- Dimostrazione
>>
>>Sia $\{ x_{i} \}_{i \in I}$ l'insieme dei valori assunti dalla v.a. $X$
>>
>>Inoltre abbiamo che $aX + b = f(X)$ dove $f(u) = au + b$
>>
>>Scriviamola come funzione di $X$:
>>
>>$$
>>\begin{align*}
>>E[aX + b] &= E[f(x)] = \sum\limits_{i}f(x_{i})P(X=x_{i})\\
>>& = a \cdot  \underbrace{\sum_{i}x_{i}P(X=x_{i})}_{E[X]} + b \cdot  \underbrace{ \sum_{i}P(X = x_{i}) }_{ 1} \\
>>& = a E[X]+b
>>\end{align*}
>>$$
>
>>[!example]- Esempio
>>$E[X] = 1000$ come calcoliamo $E[3X- 500]$ ?
>>
>>Applico la formula:
>>$$
>>E[3X-500] = 3E[X] - 500 = 3000 - 500 = 2500
>>$$
>
>>**oss:** $E[a + X + Yc] = E[a] + E[X] + E[Yc]$

---
## Funzione di Distribuzione (o Ripartizione)

>[!note] Definizione
>La funzione di distribuzione (o ripartizione) è una funzione matematica che descrive la probabilità che una variabile aleatoria assuma valori inferiori o uguali a un certo valore.
>
>**Matematicamente:**
>Data una variabile aleatoria X, la sua funzione di distribuzione è definiti come:
>
>$$
>F_{X} : \mathbb{R} \to  [0,1] \text{ con } F_{X }(a) = P(X \leq a)\ \ \forall  a \in \mathbb{R} 
>$$

>[!example]- Esempio 1
>Lanciamo un dado equilibrato a sei facce e definiamo una variabile aleatoria $X = \#\text{ facce del dado}$
>
>I valori possibili di $X$ sono 1, 2, 3, 4, 5 e 6; la probabilità di ciascun valore è la seguente:
>* $P(X=1) = 1/6$ (esce la faccia con il numero 1)
>* $P(X=2) = 1/6$ (esce la faccia con il numero 2)
>* $P(X=3) = 1/6$ (esce la faccia con il numero 3)
>* $P(X=4) = 1/6$ (esce la faccia con il numero 4)
>* $P(X=5) = 1/6$ (esce la faccia con il numero 5)
>* $P(X=6) = 1/6$ (esce la faccia con il numero 6)
>
>La funzione di distribuzione di $X$ è:
>$$
>F_{X}(x) = P(X \leq x)
>$$
>
>Calcoliamo la funzione di distribuzione per alcuni valori di x:
>$$F_{X}(1) = P(X \leq 1) = 1/6$$
>$$F_{X}(2) = P(X \leq 2) = 2/6$$
>$$F_{X}(3) = P(X \leq 3) = 3/6$$
>$$F_{X}(4) = P(X \leq 4) = 4/6$$
>$$F_{X}(5) = P(X \leq 5) = 5/6$$
>$$F_{X}(6) = P(X \leq 6) = 1$$
>
>Quindi, la funzione di distribuzione di $X$ è:
>
>$$F_{X}(a) = \begin{cases}
>0 & \text{se } a < 1 \\
>1/6 & \text{se } 1 \leq a < 2 \\
>2/6 & \text{se } 2 \leq a < 3 \\
>3/6 & \text{se } 3 \leq a < 4 \\
>4/6 & \text{se } 4 \leq a < 5 \\
>5/6 & \text{se } 5 \leq a < 6 \\
>1 & \text{se } a \geq 6
>\end{cases}$$
>

>[!example]- Esempio 2
>Estraggo 3 carte da un mazzo da 40 e definiamo una variabile aleatoria $X$ come $X :=\# \text{Carte di bastoni uscite}$ 
>
>Determinare $P_{X}​,F_{X}​,E[X]$
>
>- $P(X=0) = \frac{\binom{30}{3}}{\binom{40}{3}} = \frac{812}{1976}$
>- $P(X=1) = \frac{\binom{30}{2} \binom{10}{1}}{\binom{40}{3}} = \frac{870}{1976}$
>- $P(X=2) = \frac{\binom{30}{1} \binom{10}{2}}{\binom{40}{3}} = \frac{270}{1976}$
>- $P(X=3) = \frac{\binom{10}{3}}{\binom{40}{3}} = \frac{24}{1976}$
>
>Quindi abbiamo:
>
>$$
>E[X]=0\cdot \frac{812}{1976}+1\cdot \frac{870}{1976}+2\cdot \frac{270}{1976}+3\cdot \frac{24}{1976}=\frac{1482}{1976}
>$$
>
>E per $F(a)$:
>
>$$
>F_{X}(a)=
>\begin{cases}
>0 \ se \ a<0 \\
>\frac{812}{1976} \ se \ 0\leq a< 1 \\
>\frac{812}{1976}+\frac{870}{1976} \ se \ 1\leq a < 2 \\
>\frac{812}{1976}+\frac{870}{1976} + \frac{270}{1976} \ se \ 2\leq a < 3 \\
>1 \ se \ a\geq 3
>\end{cases}
>$$

>[!example]- Esempio 3 (calcolo inverso)
>
>Supponiamo avere una variabile aleatoria $X$ con funzione di distribuzione:
>
>$$
>F_{X}(a) = \begin{cases}
>\ 0 & \text{se }\ a<0 \\
>\frac{1}{2} & \text{se }\ 0\leq a<1 \\
>\frac{3}{5} & \text{se }\ 1\leq a<2 \\
>\frac{4}{5} & \text{se }\ 2\leq a<3 \\
>\frac{9}{10} & \text{se }\ 3\leq a<3.5 \\
>\ 1 & \text{se }\ a\geq3.5 \\
>\end{cases}
>$$
>
>Calcolare la densità di probabilità discreta $P_{X}(a)$
>
>$$
>P_{X}(a) = \begin{cases}
> \frac{1}{2} & \text{se }a = 0\\
> \frac{3}{5}- \frac{1}{2} & \text{se }a = 1 \\
> \frac{4}{5}- \frac{3}{5} & \text{se }a = 2 \\
> \frac{9}{10}- \frac{4}{5} & \text{se }a = 3 \\
>\ 1 - \frac{9}{10} & \text{se }a = 3.5
>\end{cases}
>$$
>
>Abbiamo che 
>- $P_{X}(1) = F_{X}(1) - F(0)$
>- $P_{X}(2) = F_{X}(2) - F(1)$
>- ecc
>
>**oss:** $\left( \frac{1}{2} \right) + \left( \frac{3}{5}- \frac{1}{2} \right) + \left( \frac{4}{5}- \frac{3}{5} \right) + \left(\frac{9}{10}- \frac{4}{5}\right) + \left( 1 - \frac{9}{10} \right) = 1$

---
## Varianza

>[!note] Definizione
>
>La varianza di una variabile aleatoria è una misura della dispersione dei valori della variabile rispetto al suo valore medio. In altre parole, rappresenta la quantità di variabilità o incertezza associata alla variabile
>
>**Matematicamente:**
>Sia $X$ una variabile aleatoria discreta, la varianza di $X$ è definita come: 
>
>$$
>Var(X):=E[(X-\underbrace{ EX }_{ \text{valore atteso} })^2]
>$$
>
>
>>[!example]- Esempio 1
>>Sia $X$ una variabile aleatoria che assume i valori $\{ -1,1 \}$ con probbailità:
>>- $P_{X}(1) = \frac{1}{2}$
>>- $P_{X}(-1) = \frac{1}{2}$
>>  
>>Quindi abbiamo che:
>>$$
>>E[X] = EX = 1 \cdot  \frac{1}{2} + -1 \cdot \frac{1}{2} = 0
>>$$
>>
>>$$
>>\text{Var(X)} = E[(X-EX)^{2}] = E[(X-0)^{2}] = E[X^{2}] = 1
>>$$
>
>>[!example]- Esempio 2
>>Sia $X$ una variabile aleatoria che assume i valore $\{ −3,0,1,2 \}$ con:
>>- $P_{X}(-3) = \frac{2}{10}$
>>- $P_{X}(0) = \frac{1}{10}$
>>- $P_{X}(1) = \frac{4}{10}$
>>- $P_{X}(2) = \frac{3}{10}$
>>
>>Calcoliamo $EX$ e $\text{Var}(X)$
>>- $EX = -3 \cdot \frac{2}{10} + 0 \cdot \frac{1}{10}+1\cdot \frac{4}{10} + 2 \cdot \frac{3}{10} = \frac{4}{10}$
>>  
>>$$
>>\text{Var(X)} = E\left[ \left( X - \frac{4}{10} \right)^{2} \right] = 
>>$$
>>
>>Ma come calcoliamo ($(X - \frac{4}{10})^{2}$? Dobbiamo vedere i singoli casi:
>>- $X = 3 \to (x-0.4)^{2} = (-3 - 0.4)^{2} = 11.56$
>>- $X = 0 \to (x-0.4)^{2} = (0-0.4)^{2} = 0.16$
>>- $X = 1 \to (x-0.4)^{2} = (1-0.4)^{2} = 0.36$
>>- $X = 2 \to (x-0.4)^{2} = (2-0.4)^{2} = 2.56$
>>  
>>Quindi otteniamo:
>>$$
>>(X - 0.4)^{2} = \begin{cases}
>>11.56 &\text{con probabilità} \frac{2}{10}\\
>>0.16 &\text{con probabilità} \frac{1}{10}\\
>>0.36 &\text{con probabilità} \frac{4}{10}\\
>>2.46 &\text{con probabilità} \frac{3}{10}\\
>>\end{cases}
>>$$
>>
>>Allora:
>>$$
>>\text{Var}(X) = E[(X-0.4)^{2}] = 11.56 \cdot  0.2 + 0.16 \cdot 0.1 + 0.36 \cdot 0.4 + 2.56 \cdot  0.3 = 3.24
>>$$

>[!note] Calcolo Alternativo
>È possibile calcolare la [[#Varianza]] anche come:
>
>$$
>\text{Var}(X) = E[X^{2}] - (EX)^{2}
>$$
>
>>[!example]- Esempio
>>$X$ assume valori $\{−1,0,2,3\}$ e abbiamo che:
>>- $P(-1) = 0.1$
>>- $P(0) = 0.2$
>>- $P(2) = 0.2$
>>- $P(3) = 0.5$
>>
>>  
>>Calcoliamo: $\text{Var(X)} = E[X^{2}] - (EX)^{2}$
>>
>>$$
>>\begin{align*}
>> &- \ \ EX = −1 \cdot 0.1 + 0 \cdot 0.2 + 2 \cdot 0.2 + 3 \cdot  0.5 = 1.8\\
>> &- \ \ E[X^{2}] = (-1)^{2}P(-1) + (0)^{2}P(0) + (2)^{2}P(2) + (3)^{3}P(3) = 5.4
>>\end{align*}
>>$$
>>
>>Quindi:
>>$$
>>\text{Var}(X) = 5.4 - (1.8)^{2} = 2.16
>>$$
>>
>>>**Utilizzando l'altro metodo:**
>>>$$
>>>\text{Var}(X) = E((X−EX)^{2}) = (−1−1.8)^{2}P(−1)+(0−1.8)^{2}P(0)+(2−1.8)^{2}P(2)+(3−1.8)^{2}P(3)
>>>$$

>[!danger] Prop (non lineare)
>Data $X$ v.a. discreta e dati $a,b \in \mathbb{R}$ vale:
>
>$$
>\text{Var}(aX + b) = a^{2}\text{Var}(X)
>$$
>
>Notiamo che le variabili addizionali vengono eliminate e quelle moltiplicative aplificate
>
>>[!example] Esempio
>>***DA FAREEE metti esempio fatto con prof sostitutivo***
>
>**Approfondimento:** [[Perché le costanti additive non importano nella varianza?]]

---
## Deviazione Quadrata

>[!note] Definizione
>
>La deviazione quadrata di una variabile aleatoria è una misura della dispersione dei valori della variabile rispetto al suo valore medio.
>
>Non è altro che una misura più intuitiva della dispersione rispetto alla [[#Varianza]], poiché è espressa nella stessa unità di misura della variabile aleatoria.
>
>**Matematicamente:**
>Sia $X$ una variabile aleatoria discreta, la deviazione quadrata di $X$ è definita come:
>
>$$
>\sigma(X) := \sqrt{\text{Var}(X)} = \sqrt{E[(X-EX)^2]}
>$$
>
>>[!example]- Esempio 1
>>Sia $X$ una variabile aleatoria che assume i valori $\{ -1,1 \}$ con probabilità:
>>- $P_{X}(1) = \frac{1}{2}$
>>- $P_{X}(-1) = \frac{1}{2}$
>>  
>>Quindi abbiamo che:
>>$$
>>E[X] = EX = 1 \cdot  \frac{1}{2} + -1 \cdot \frac{1}{2} = 0
>>$$
>>
>>$$
>>\text{Var(X)} = E[(X-EX)^{2}] = E[(X-0)^{2}] = E[X^{2}] = 1
>>$$
>>
>>$$
>>\sigma(X) = \sqrt{Var(X)} = \sqrt{1} = 1
>>$$
>
>>[!example]- Esempio 2
>>Sia $X$ una variabile aleatoria che assume i valore $\{ −3,0,1,2 \}$ con:
>>- $P_{X}(-3) = \frac{2}{10}$
>>- $P_{X}(0) = \frac{1}{10}$
>>- $P_{X}(1) = \frac{4}{10}$
>>- $P_{X}(2) = \frac{3}{10}$
>>
>>Calcoliamo $EX$ e $\text{Var}(X)$
>>- $EX = -3 \cdot \frac{2}{10} + 0 \cdot \frac{1}{10}+1\cdot \frac{4}{10} + 2 \cdot \frac{3}{10} = \frac{4}{10}$
>>  
>>$$
>>\text{Var(X)} = E\left[ \left( X - \frac{4}{10} \right)^{2} \right] = 3.24
>>$$
>>
>>$$
>>\sigma(X) = \sqrt{Var(X)} = \sqrt{3.24} \approx 1.80
>>$$

>[!danger] Prop (non lineare)
>Sia $X$ variabile aleatoria, $a$ e $b$ numeri in $\mathbb{R}$, allora:
>
>$$
>\sigma(aX + b) = |a| \cdot  \sigma(X)
>$$
>
>>[!example] Esempio
>>***DA FAREEE metti esempi  visto con il prof sostitutivo*** 

---
## Funzione di Variabile Aleatoria

>[!note] Definizione
>Dati $(S, P)$ e $X:S\to \mathbb{R}$ 
>
>Sia $f:\mathbb{R} \to \mathbb{R}$, Denoto con $f(X)$ la **variabile aleatoria** $f \circ X$ ovvero:
>
>$$
>S \overset{X}{\to} \mathbb{R} \overset{f}{\to} \mathbb{R}
>$$
>
>>**Osservazioni:**
>>- $f(X): S \to \mathbb{R}$ è una variabile aleatoria
>>- $X: S \to \mathbb{R}$ assume i valori $\{ X_{i}: i \in I\}$
>>- $f(X) = f \circ X:S\to \mathbb{R}$ assume i valori $\{ f(X_{i}: i \in I) \}$
>  
>>[!example]- Esempio
>>Lanciamo 10 volte una moneta e definiamo la v.a. $X$ come $X := \# \text{Teste Uscite}$
>>- Vinco 2 euro per ogni testa
>>- Perdo 1 euro per ogni croce
>>
>>Definiamo una v.a. $Y$ come $Y := \text{Guadagno/perdita dei 10 lanci}$
>>
>>Come si può notare $Y$ dipende strettamente da il valore di $X$ quindi è possibile definire $Y$ come $f(x)$, in particolare:
>>
>>$$
>>Y = f(x) = 2X - 1(10-X) = 3X -10
>>$$

>[!warning] Calcolo del valore atteso di $f(X)$
>
>Il 2° metodo è più semplice da usare
>
>>**1° Metodo**
>>Chiamiamo i possibili valori di $f(X)$ come $\{ y_{j}: i \in J\}$ e calcoliamo:
>>
>>$$
>>P(f(X) = y_{i}) \forall  j \in J 
>>$$
>>
>>Per definizione di [[#Valore Atteso]] otteniamo che:
>>
>>$$
>>E[f(X)] = \sum_{j} y_{j} \cdot  P(f(X) = y_{j})
>>$$
>>
>Metodo 1 consiste nel prendere tutti i valori possibili di $f(X)$, ovvero $y_{j}$, e moltiplicarli per la probabilità che la funzione assuma quel valore, ovvero $P(f(X) = y_{j})$. Infine, si sommano tutti questi prodotti per ottenere il valore atteso di $f(X)$.
>
>>**2° Metodo (Teorema)**
>>
>>Sia $X$ v.a. discreta che assume valori $\{ X_{i} \}_{i \in I}$ e sia $f: \mathbb{R} \to \mathbb{R}$, allora:
>>$$
>>E[f(X)] = \sum_{i\in I} f(X_{i}) \cdot P(X = X_{i})
>>$$
>>
>>Metodo 2 consiste nel prendere tutti i valori che la variabile aleatoria $X$ può assumere ($X_{i}$), applicare la funzione $f$ a questi valori per ottenere $f(X_{i})$, e poi moltiplicare ogni valore di $f(X_{i})$ per la probabilità che la variabile aleatoria $X$ assuma quel valore ($P(X = X_{i})$). Infine, si sommano tutti questi prodotti per ottenere il valore atteso di $f(X)$.
>>
>
>>[!example]- Esempio (molto utile)
>>Data la v.a. $X$ che assume i valori $-1,0,3$ con rispettive probabilità 0.2, 0.5, 0.3.
>>
>>Calcolare $E((X-1)^{2})$
>>
>>>**Metodo 1**
>>>
>>>$$
>>>Y = (X-1)^{2} \text{assume i valori} \begin{cases}
>>>4 &\text{se }X=-1 \\
>>>4 &\text{se }X=-3 \\
>>>1 &\text{se }X=0
>>>\end{cases}
>>>$$
>>>
>>>- $P(Y=4) = P(X= -1) + P(X=3) = 0.2 + 0.3 = 0.5$
>>>- $P(Y=1) = P(X=0) = 0.5$
>>> 
>>>$$
>>>E[Y] = 4 \cdot 0.5 + 1 \cdot 0.5 = 2.5
>>>$$
>>
>>>**Metodo 2:**
>>>
>>>$$
>>>\begin{align*}
>>>E[Y] &= f(-1) \cdot  P(X = -1) + f(0)\cdot P(X=0) + f(3)\cdot P(X=3)\\
>>>&\ \ |\\
>>>&= (-1-1)^{2} \cdot 0.2 + (0-1)^{2}\cdot 0.5 + (3-1)\cdot 0.3\\
>>>&\ \ |\\
>>>&= 0.8 + 0.5 + 1.2 = 2.5
>>>\end{align*}
>>>$$

---
## Variabile Aleatoria di Bernoulli

Una variabile di Bernoulli è una variabile aleatoria che può assumere solo due valori possibili, solitamente indicati come 0 e 1, o come "successo" e "fallimento".

>[!note] Definizione Matematica
>Una v.a. $X$ è detta di Bernoulli di parametro $p \in [0,1]$ se:
>- $P(X=1)=p$ 
>- $P(X=0)=1−p$

>[!warning] Osservazioni
>$$
>\begin{align*}
>&1.\ \ \textcolor{orange}{E[X]} = 1 \cdot  P(X=1) + 0 \cdot P(X=0) = \textcolor{orange}{p}\\
>&2.\ \ \textcolor{orange}{E[X^{2}]} = 1^{2} \cdot  P(X=1) + 0^{2} \cdot P(X=0) = \textcolor{orange}{p}\\
>&3.\ \ \textcolor{orange}{\text{Var}(X)} = E[X^{2}]-(EX)^{2} = p-p^{2} = \textcolor{orange}{p(1-p)}\\
>\end{align*}
>$$

---
## Variabile Aleatoria Binomiale

Una **variabile aleatoria binomiale** è una variabile aleatoria che rappresenta il *numero di successi in una sequenza di prove indipendenti*, ognuna delle quali ha due possibili risultati: successo o insuccesso.

La variabile aleatoria binomiale è caratterizzata da due parametri:
* $n$ -> il numero di prove
* $p$ -> la probabilità di successo in ogni prova

La variabile aleatoria binomiale può assumere valori interi compresi tra $0$ e $n$, dove $0$ rappresenta il numero di successi in nessuna delle prove e $n$ rappresenta il numero di successi in tutte le prove.

>[!note] Notazione
>Indichiamo una v.a binomiale $X$ di parametri $n,p$ con:
>$$
>X = \text{Bin}(n,p)
>$$

>[!danger] Calcolo Probabilità
>La probabilità di ottenere $k$ successi in $n$ prove è data dalla formula:
>
>$$
>P(X=k) = \binom{n}{k}\cdot  p^k \cdot  (1-p)^{n-k}
>$$

>[!danger] Calcolo Valore Atteso
>$$
>E[X] = n \cdot p
>$$

>[!danger] Varianza
>$$
>\text{Var}(X) = n\cdot p\cdot (1−p)
>$$

>[!example]- Esempio
>Lancio cinque volte una moneta. Sia $X$ v.a definita come $X:=\text{Teste Uscite}$
>
>Determinare:
>1. Probabilità discreta di $X$
>2. $E[X]$
>3. $\text{Var}(X)$
>4. $\sigma(X)$
>   
>**oss:** $X$ è una v.a. binomiale infatti possiamo definirla come: $X = \text{Bin}\left( 5, \frac{1}{2} \right)$
>
>**1.  Probabilità Discreta:**
>Sappiamo che $X$ può assume i valori $0,1,2,3,4,5$ quindi per questi valori $k$ calcoliamo:
>$$
>\begin{align*}
>P(X=k) &= \binom{n}{k} \cdot  p^{k} \cdot (1-p)^{n-k}\\
>& \ \ |\\
>&= \binom{5}{k}\cdot  (\frac{1}{2})^{k} \cdot (\frac{1}{2})^{5-k} \\
>& \ \ |\\
>&= \binom{5}{k}\cdot  (\frac{1}{2})^{5} \\
>& \ \ |\\
>&= \binom{5}{k}\cdot\frac{1}{32} \\
>\end{align*}
>$$
>
>$$
>P(0) = \binom{5}{0}  \cdot  \frac{1}{32} = \frac{1}{32} \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ P(1) = \binom{5}{1}  \cdot  \frac{1}{32} = \frac{5}{32} \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ P(2) = \binom{5}{2}  \cdot  \frac{1}{32} = \frac{10}{32}
>$$
>
>$$
>P(3) = \binom{5}{3}  \cdot  \frac{1}{32} = \frac{10}{32} \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ P(4) = \binom{5}{4}  \cdot  \frac{1}{32} = \frac{5}{32} \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ P(5) = \binom{5}{2}  \cdot  \frac{1}{32} = \frac{1}{32}
>$$
>
>**2. Valore Atteso:** $E[X] = n\cdot p = 5 \cdot \frac{1}{2} = 2.5$
>
>**3. Varianza:** $\text{Var}(X) = n \cdot p \cdot (1-p) = 5 \cdot \frac{1}{2} \cdot \frac{1}{2} = 1.25$
>
>**4. Deviazione Quadrata:**  $\sigma(X) = \sqrt{ \text{Var}(X) } = \sqrt{ 1.25 } = 1.118$

---
## Variabile Aleatoria di Poisson

Una variabile aleatoria di Poisson è una variabile aleatoria che rappresenta il numero di eventi che si verificano in un intervallo di tempo o spazio fissato, dove gli eventi sono indipendenti e hanno una probabilità costante di verificarsi.

>[!note] Notazione
>Indichiamo una v.a di Poisson $X$ di parametro λ con:
>$$
>X = \text{Pois}(\lambda)
>$$
>
>Dove λ (lambda) indica: la media del numero di eventi che si verificano nell'intervallo di tempo o spazio fissato
>
>>**oss:** La variabile aleatoria di Poisson può assumere valori interi non negativi (0, 1, 2, ...).

### Formule

>[!danger] Calcolo Probabilità
>La probabilità di ottenere $k$ eventi è data dalla formula:
>
>$$
>P_{X}(k) = P(X=k) = \frac{\lambda^k \cdot e^{-\lambda}}{k!}
>$$
>
>Dove:
>- $P_{X}(k) \geq 0 \forall  k = 0,1,2, \dots$
>- $\sum^{\infty}_{k=0} P_{X}(k)=1$

>[!danger] Calcolo Valore Atteso
>$$
>E[X] = \lambda
>$$

>[!danger] Varianza
>$$
>\text{Var}(X) = \lambda
>$$

>[!example]- Esempio
>Supponiamo di avere una linea di produzione dove si verificano errori con una media di 2 errori all'ora ($\lambda = 2$). Sia $X$ la variabile aleatoria che rappresenta il numero di errori che si verificano in un'ora.
>
>Determinare:
>1. Probabilità di ottenere 0 errori
>2. Probabilità di ottenere 1 errore
>3. Probabilità di ottenere 2 errori
>4. Valore atteso di $X$
>5. Varianza di $X$
>
>**1. Probabilità di ottenere 0 errori:**
>$$
>P(X=0) = \frac{\lambda^0 \cdot e^{-\lambda}}{0!} = e^{-2} \approx 0,135
>$$
>
>**2. Probabilità di ottenere 1 errore:**
>$$
>P(X=1) = \frac{\lambda^1 \cdot e^{-\lambda}}{1!} = 2e^{-2} \approx 0,271
>$$
>
>**3. Probabilità di ottenere 2 errori:**
>$$
>P(X=2) = \frac{\lambda^2 \cdot e^{-\lambda}}{2!} = \frac{4}{2}e^{-2} \approx 0,271
>$$
>
>**4. Valore atteso di $X$:**
>$$
>E[X] = \lambda = 2
>$$
>
>**5. Varianza di $X$:**
>$$
>\text{Var}(X) = \lambda = 2
>$$

## Approssimazione di variabile di Binomiale con Poisson

Se $n$ è molto grande e $p$ è piccolo, la variabile aleatoria binomiale $\text{Bin}(n,p)$ può essere approssimata dalla variabile aleatoria di Poisson con parametro $\lambda = np$

$$
\text{Pois}(n \cdot p) \approx \text{Bin}(n,p) \iff \text{Pois}(\lambda) \approx \text{Bin}\left( n,\frac{\lambda}{n}​ \right)
$$

Questa approssimazione è nota come "**legge dei piccoli numeri**" e si basa sul fatto che quando $n$ è molto grande e $p$ è piccolo, la **probabilità di successo in una singola prova è molto piccola**, e quindi la variabile aleatoria binomiale può essere approssimata da una variabile aleatoria di Poisson.

>[!warning] Teorema: Legge dei Grandi Numeri
>Dato $n \in \{ 1,2,\dots \}$ si $P_{n} \in [0,1]$ tale che:
>$$
>\exists \lim_{ n \to \infty } n \cdot  P_{n} =: \lambda > 0
>$$
>
>Allora $X_{n}=\text{Bin}(n , P_{n})$ e $Z = \text{Pos}(\lambda)$ allora:
>$$
>\lim_{ n \to \infty } P(X_{n} = k ) = P(Z=k)\ \ \ \forall k \in \{ 0,1,2,\dots \} 
>$$
>
>Quindi per $n$ grande possiamo approssimare $P(X_{n} = k) \approx P(Z=K)$, quindi in alcune situazioni abbiamo che:
>$$
>\text{Bin}(n,p) \approx \text{Pois}(\lambda)
>$$
>
>Dove presi $n,\ p,\ \lambda$ abbiamo che:
>- $n\gg 1$ ($n$ molto più grande di 1)
>- $np \approx \lambda$ (quindi $p \approx \frac{y}{n}$)
>
>>**oss:** Cosa si intende per $\text{Bin}(n,p) \approx \text{Pois}(\lambda)$?
>>
>>$$
>>P(X = k) \approx P(Z=k)\ \ \forall k = 0,1,2,\dots 
>>$$
>>
>>Dove $X= \text{Bin(n,p)}$ e $Z =\text{Pois}(\lambda)$.
>
>>[!warning] Dim

>[!example]- Esempio Astratto
>Prendiamo la pagina di un libro e consideriamo la probabilità che un carattere venga stampato in modo errato. 
>
>Quindi abbiamo una v.a. binomiale infatti un numero di prove $n$ e due esiti, successo se stampato male e insuccesso altrimenti.
>
>Notiamo che $n$ è il numero di caratteri ed è molto alto all’interno di una pagina, e $p$ possiamo assumerla piccola.
>
>Possiamo quindi assumere $\text{Bin}(n,p) \approx Poisson(\lambda)$ dove $\lambda=n\cdot p$

>[!example]- Esempio Concreto
>Supponiamo che il numero di errori tipografici per pagina sia approssimato da $\text{Pois}\left( \frac{1}{2} \right)$
>
>**Versione 1:**
>Trovare la probabilità che ci sia almeno un errore a pagina 20.
>
>Definiamo una v.a. aleatoria $Z$ tale che  $Z:=\text{numero di errori a pagina 20}$, abbiamo che:
>$$
>\begin{align*}
>&- \ \ \ Z = \text{Pois}(\lambda) \text{ con } \lambda=\frac{1}{2}\\
>&- \ \ \ P(z = k) = e^{-1/2} \cdot \left( \frac{1}{2} \right)^{k} \cdot \frac{1}{k!}
>\end{align*}
>$$
>
>Possiamo considerare il fatto che ci sia almeno un errore come l’evento complementare di non ci sono errori, quindi possiamo calcolare:
>$$
>P(Z\geq 1) = 1 - P(Z=0) = 1 - e^{-\frac{1}{2}} \cdot \left( \frac{1}{2} \right)^{0} \cdot  \frac{1}{0!} = 1 - e^{- \frac{1}{2} } \approx 0.393
>$$
>
>**Versione 2:**
>Trovare la probabilità che ci sia esattamente 4 errori a pagina 20.
>
>Dobbiamo quindi calcolare:
>$$
>P(Z=4) = e^{-\frac{1}{2}} \cdot  \left( \frac{1}{2} \right)^{4} \cdot  \frac{1}{4!} = \frac{1}{\sqrt{ e }} \cdot \frac{1}{16} \cdot \frac{1}{24} \approx 0.00158 
>$$
>
>**La Poisson approssima una binomiale** $\text{Pois}(\lambda) \approx \text{Bin}\left( n, \frac{\lambda}{n} \right)$

---
## Variabile Geometrica


---
## Binomiale negativa 


>[!example] Esempio
>
>***Aggiungi esempio partite basket (ipad)***



