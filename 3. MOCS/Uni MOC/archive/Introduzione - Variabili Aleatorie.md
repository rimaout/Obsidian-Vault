---
type: Uni Note
class:
  - "[[Calcolo delle Probabilità (class)]]"
academic year: 2024/2025
related: 
completed: true
created: 2024-10-29T15:31
updated: 2025-02-17T17:18
---
>[!abstract] Related
>- [[Calcolo delle Probabilità (class)]]

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
>Il valore atteso di una variabile aleatoria discreta rappresenta il valore medio che ci si aspetta di ottenere se si ripetesse un esperimento aleatorio un numero infinito di volte
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
>il valore atteso è lineare
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
>>**oss:** $E[aX + bY + y] = aE[X] + bE[Y] + c$

---
## Funzione di Distribuzione (o Ripartizione)

>[!note] Definizione
>La funzione di distribuzione (o ripartizione) è una funzione matematica che descrive la probabilità che una variabile aleatoria assuma valori inferiori o uguali a un certo valore.
>
>**Matematicamente:**
>Data una variabile aleatoria $X$, la sua funzione di distribuzione è definiti come:
>
>$$
>F_{X} : \mathbb{R} \to  [0,1] \text{ con } F_{X}(a) = P(X \leq a)\ \ \forall a \in \mathbb{R} 
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
>$$
>F_{X}(a) = \begin{cases}
>0 & \text{se } a < 1 \\
>1/6 & \text{se } 1 \leq a < 2 \\
>2/6 & \text{se } 2 \leq a < 3 \\
>3/6 & \text{se } 3 \leq a < 4 \\
>4/6 & \text{se } 4 \leq a < 5 \\
>5/6 & \text{se } 5 \leq a < 6 \\
>1 & \text{se } a \geq 6
>\end{cases}
>$$

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
>Notiamo che le variabili addizionali vengono eliminate e quelle moltiplicative amplificate, la varianza è quadratica.
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

