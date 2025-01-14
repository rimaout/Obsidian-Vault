---
type: Uni Note
class: "[[Calcolo delle Probabilità (class)]]"
academic year: 2024/2025
related:
  - "[[Variabili Aleatorie]]"
completed: true
created: 2024-11-28T11:46
updated: 2025-01-08T10:48
---

>[!abstract] Related
>- [[Variabili Aleatorie]]
>- [[Calcolo delle Probabilità (class)]]

---
## Definizione

Una variabile aleatoria congiunta è una variabile aleatoria che rappresenta il comportamento di due o più variabili aleatorie correlate.

>[!note] Notazione
>
>Siano $X$ e $Y$ due variabili aleatorie definite su uno stesso spazio campionario. Indichiamo con  $(X, Y)$ la variabile aleatoria congiunta ovvero una funzione che associa ad ogni punto dello spazio campionario un valore della coppia $X,Y$.

---
## Densità di Probabilità Congiunta

>[!note] Definizione
>
>Date due v.a $X$ e $Y$ definite sullo stesso spazio campionario ($X: S \to \mathbb{R}$ e $Y: S \to \mathbb{R}$) ed entrambe discrete dove:
>- $X$ ha valori in $\{ x_{i} \}_{i \in I}$ 
>- $Y$ ha valori in $\{ y _{j}\}_{j \in J}$
>
>La densità di probabilità discreta disgiunta $P_{X,Y}$ è la funzione:
>
>$$
>P_{X \times Y}: \{ x_{i} \}_{i \in I} \times \{ y_{j} \}_{j \in J} \to  [0,1]
>$$
>
>Data da $P_{X, Y} (x_{i}, y_{j} )=P(X= x_{i}, Y = y_{j})$

>[!warning] Proprietà
>- $P_{X,Y}(x_{i}, y_{i}) \in [0,1]$
>- $\sum_{i\in I}\sum_{j \in J} P_{X,Y}(x_{i}, y_{j}) = 1$

>[!example]- Esempio 1
>
>Supponiamo di lanciare un dado una sola volta, chiamiamo 
>- $X := \# \text{Lanci in cui ho faccia pari}$
>- $Y := \# \text{Lanci in cui esce multiplo di 3}$. 
>
>Possiamo osservare che:
>- $X$ assume i valori $\{ 0,1 \}$
>- $Y$ assume i valori $\{ 0,1\}$
>  
>
>
>Dobbiamo riempire la tabella per $P_{X,Y}$
>
>| X/Y | 0              | 1              |
>| --- | -------------- | -------------- |
>| 0   | $P_{X,Y}(0,0)$ | $P_{X,Y}(0,1)$ |
>| 1   | $P_{X,Y}(1,0)$ | $P_{X,Y}(1,1)$ |
>
>$P_{X,Y}(0,0)$: Probabilità che il dado mostri una faccia dispari e non un multiplo di 3. Le facce dispari sono 1, 3, 5. Le facce non multipli di 3 tra queste sono 1 e 5. Quindi:
>- Possibilità: $(1, 5)$ → 2 casi
>- Probabilità: $\frac{2}{6} = \frac{1}{3}$
>
>$P_{X,Y}(0,1)$: Probabilità che il dado mostri una faccia dispari e un multiplo di 3. L'unico multiplo di 3 tra le facce dispari è 3. Quindi:
>- Possibilità: \(3\) → 1 caso
>- Probabilità: $\frac{1}{6}$
>
>$P_{X,Y}(1,0)$: Probabilità che il dado mostri una faccia pari e non un multiplo di 3. Le facce pari sono 2, 4, 6. Le facce pari che non sono multipli di 3 sono 2 e 4. Quindi:
>- Possibilità: \(2, 4\) → 2 casi
>- Probabilità: $\frac{2}{6} = \frac{1}{3}$
>
>$P_{X,Y}(1,1)$: Probabilità che il dado mostri una faccia pari e un multiplo di 3. L'unico multiplo di 3 tra le facce pari è 6. Quindi:
>- Possibilità: $(6)$ → 1 caso
>- Probabilità: $\frac{1}{6}$
>
>Ora possiamo riempire la tabella:
>
>| X/Y | 0              | 1              |
>| --- | -------------- | -------------- |
>| 0   | $\frac{1}{3}$  | $\frac{1}{6}$  |
>| 1   | $\frac{1}{3}$  | $\frac{1}{6}$  |

>[!example]- Esempio 2
>Supponiamo di lanciare un dado 2 volte, chiamiamo 
>- $X := \# \text{Lanci in cui ho faccia pari}$
>- $Y := \# \text{Lanci in cui esce multiplo di 3}$. 
>  
>Possiamo osservare che:
>- $X$ assume i valori $\{ 0,1,2 \}$
>- $Y$ assume i valori $\{ 0,1,2 \}$
>  
>**Come calcoliamo $P_{X,Y}​$?**
>
>Dobbiamo riempire questa tabella che copre tutti i casi possibili:
>
>| X/Y | 0        | 1        | 2      |
>| --- | -------- | -------- | -------- |
>| 0   | $P_{X,Y}(0,0)$ | $P_{X,Y}(0,1)$ | $P_{X,Y}(0,2)$ |
>| 1   | $P_{X,Y}(1,0)$ | $P_{X,Y}(1,1)$ | $P_{X,Y}(1,2)$ |
>| 2   | $P_{X,Y}(2,0)$ | $P_{X,Y}(2,1)$ |  $P_{X,Y}(2,2)$ |
>
>* $P_{X,Y}(0,0) = P((1,5),\ (5,1),\ (1,1),\ (5,5)) = \frac{4}{36}$
>* $P_{X,Y}(0,1) = P((1,3),\ (5,3),\ (1,6),\ (5,6),\ (3,1),\ (6,1),\ (3,5),\ (6,5)) = \frac{8}{36}$
>* $P_{X,Y}(0,2) = P() = \frac{0}{36}$
>* $P_{X,Y}(1,0) = P((2,1),\ (2,5),\ (4,1),\ (4,5),\ (6,1),\ (6,5),\ (1,2),\ (5,2),\ (1,4),\ (5,4)) = \frac{10}{36}$
>* $P_{X,Y}(1,1) = P((2,3),\ (2,6),\ (4,3),\ (4,6),\ (6,3),\ (6,6),\ (3,2),\ (6,2),\ (3,4),\ (6,4)) = \frac{10}{36}$
>* $P_{X,Y}(1,2) = P() = \frac{0}{36}$
>* $P_{X,Y}(2,0) = P((2,2),\ (2,4),\ (4,2),\ (4,4),\ (6,2),\ (6,4),\ (2,6),\ (4,6)) = \frac{8}{36}$
>* $P_{X,Y}(2,1) = P((2,6),\ (6,2),\ (4,6),\ (6,4)) = \frac{4}{36}$
>* $P_{X,Y}(2,2) = P() = \frac{0}{36}$
>  
>| X/Y | 0               | 1               | 2              |
>| --- | --------------- | --------------- | -------------- |
>| 0   | $\frac{4}{36}$  | $\frac{8}{36}$  | $\frac{0}{36}$ |
>| 1   | $\frac{10}{36}$ | $\frac{10}{36}$ | $\frac{0}{36}$ |
>| 2   | $\frac{8}{36}$  | $\frac{4}{36}$  | $\frac{0}{36}$ |
>
>**Metodo alternativo:** fare la tabella con i possibili valori dello spazio campionario, in questo caso un 6x6 e poi inserire in ogni casella la coppia di valori $(x,y)$, poi contiamo quante caselle per ogni coppia di valori.
>
>
>|  | 1 | 2 | 3 | 4 | 5 | 6 |
>| --- | --- | --- | --- | --- | --- | --- |
>| 1 | (0,0) | (1,0) | (0,1) | (1,0) | (0,0) | (1,1) |
>| 2 | (1,0) | (2,0) | (1,1) | (2,0) | (1,0) | (2,1) |
>| 3 | (0,1) | (1,1) | (0,2) | (1,1) | (0,1) | (1,2) |
>| 4 | (1,0) | (2,0) | (1,1) | (2,0) | (1,0) | (2,1) |
>| 5 | (0,0) | (1,0) | (0,1) | (1,0) | (0,0) | (1,1) |
>| 6 | (1,1) | (2,1) | (1,2) | (2,1) | (1,1) | (2,2) |
>Ora, contiamo quante caselle per ogni coppia di valori:
>* $(0,0)$: 4 caselle
>* (0,1): 4 caselle
>* (0,2): 0 caselle
>* (1,0): 6 caselle
>* (1,1): 6 caselle
>* (1,2): 0 caselle
>* (2,0): 4 caselle
>* (2,1): 4 caselle
>* (2,2): 0 caselle
>
>Quindi, la tabella della densità di probabilità discreta disgiunta $P_{X,Y}$ è:
>  
>| X/Y | 0              | 1              | 2              |
>| --- | -------------- | -------------- | -------------- |
>| 0   | $\frac{4}{36}$ | $\frac{4}{36}$ | $\frac{0}{36}$ |
>| 1   | $\frac{6}{36}$ | $\frac{6}{36}$ | $\frac{0}{36}$ |
>| 2   | $\frac{4}{36}$ | $\frac{4}{36}$ | $\frac{0}{36}$ |
>
>>***Attenzione:*** Ci sono sicuramente degli errori perché la tabella non sono uguali ma in generale il ragionamento è giusto

>[!example]- Esempio 3
>
>![[Pasted image 20241202101734.png]]

---
## Densità di probabilità Marginale

In una v.a. discreta congiunta, le densità che la compongono vengono chiamata **marginali** e conoscendo la congiunta possiamo calcolare le marginali

>*oss:* non vale il contrario, non è possibile ricavare il valore della densità di probabilità congiunta conoscendo il valore delle marginali

>[!note] Calcolo
>
>Marginali della variabile aleatoria congiunta $(X,Y)$
>
>- $P_{X}​(x_{i}​) = \sum_{j\in J} P_{X,Y}​(x_{i}​,y_{j}​)$
>- $P_{Y}​(y_{j}​) = \sum_{i \in I} P_{X,Y}​(x_{i}​,y_{j}​)$
 
>[!example]- Esempio
>Ho due v.a. $X$ e $Y$ su $S$, dove:  
>- $X$ assume valori $−2,0,5$
>- $Y$ assume valori $4,9$
>  
>Inoltre $P_{X,Y}$​ è data da:
>
>| X/Y | 4 | 9 |
>| --- | --- | --- |
>| $-2$ | $\frac{1}{10}$ | $\frac{2}{10}$ |
>| $0$  | $\frac{0}{10}$ | $\frac{1}{10}$ |
>| $5$  | $\frac{3}{10}$ | $\frac{3}{10}$ |
>
>**Determinare pX​ e pY​.**
>
>Ricordiamo la formula:
>
>$$
>P_{X}(x_{i})=\sum_{j}P_{X,Y}(x_{i},y_{j})
>$$
>
>Quindi calcolando $P_{X}$
>
>$$
>P_{X}(-2) = P_{X,Y}(-2,4)+P_{X,Y}(-2,9) = \frac{1}{10}+\frac{2}{10}=\frac{3}{10}
>$$
>
>$$
>P_{X}(0) = \frac{0}{10}+\frac{1}{10} = \frac{1}{10}
>$$
>
>$$
>P_{X}(-2,9) = \frac{1}{10}+\frac{2}{10} = \frac{3}{10}
>$$
>
>$$
>P_{X}(5) = \frac{3}{10}+\frac{3}{10} = \frac{6}{10}
>$$
>
>Mentre per la $P_{Y}$:
>
>$$
>P_{Y}(4) = P_{XY}(-2,4)+P_{XY}(0,4)+P_{XY}(5,4) = \frac{1}{10}+\frac{0}{10}+\frac{3}{10}=\frac{4}{10}
>$$
>
>$$
>P_{Y}(9) = \frac{2}{10}+\frac{1}{10}+\frac{3}{10} = \frac{6}{10}
>$$

>[!example]- Esempio palline con rimpiazzo
>Abbiamo un’urna con 6 palline numerate da 1 a 6, estraiamo 2 palline con rimpiazzo e definiamo:
>
>$$
>\begin{align*}
>&X := \text{Numero della prima pallina}\\
>&Y := \text{Numero della seconda pallina}
>\end{align*}
>$$
>
>Quindi $X$ assume valori in $\{ 1,2,3,4,5,6 \}$ e con $P_{X}(k)= \frac{1}{6}$ per ogni $k$ da 1 a 6 (stessa cosa per $Y$)
>
>La congiunta $(X,Y)$ assume valori $(a,b)$ con $a,b \in \{ 1,2,3,4,5,6 \}$
>
>$$
>P_{X,Y}(X=a,Y=b) = \frac{1}{36}\ \ \ \ \forall (a,b) \in \{ 1,2,3,4,5,6 \}^{2}
>$$

>[!example]- Esempio palline senza rimpiazzo
>Abbiamo un’urna con 6 palline numerate da 1 a 6, estraiamo 2 palline con rimpiazzo e definiamo:
>
>$$
>\begin{align*}
>&X := \text{Numero della prima pallina}\\
>&Y := \text{Numero della seconda pallina}
>\end{align*}
>$$
>
>Quindi $X$ assume valori in $\{ 1,2,3,4,5,6 \}$ e con $P_{X}(k)= \frac{1}{6}$ per ogni $k$ da 1 a 6 (stessa cosa per $Y$)
>
>La congiunta $(X,Y)$ assume valori $(a,b)$ con $a,b \in \{ 1,2,3,4,5,6 \}$
>
>$$
>P_{X,Y}(X=a,Y=b) = \begin{cases}
\frac{1}{30} & \text{se } a,b \in \{ 1,\dots,6 \} \text{ e } a \not = b\\ \\
>0 & \text{se }a,b \in \{ 1,\dots,6 \} \text{ e } a = b
>\end{cases} 
>$$

>***oss:*** Notiamo quindi che negli ultimi due esperimenti le due marginali sono uguali ma la congiunta dipende dall’esperimento e quindi cambia.

---
## Valore Atteso

>[!note] Calcolo
>Siano $X$ e $Y$ v.a. discrete e sia $f:\mathbb{R}^{2} \to R$, allora:
>$$
>E[f(X,Y)] = \sum_{i\in I} \sum_{j\in J} f(x_{i}, y_{j}) P_{X,Y} (x_{i}, y_{j})
>$$
>
>Dove 
>- $\{ X_{i} \}_{i \in I}$ è l'insieme dei possibili valori di $X$
>- $\{ Y_{j} \}_{j \in J}$ è l'insieme dei possibili valori di $Y$
>
>>[!example]- Esempio
>>
>>Data $f:\mathbb{R}^{2}\to R$ definita come $f(a,b) = a^{2}b$ e le v.a $X,Y$  tali che:
>>
>>![[Pasted image 20241125150221.png|200]]
>>
>>Calcolare $E[X^{2}Y]$:
>>
>>![[Pasted image 20241125151035.png|800]]

>[!warning] Prop. Somma
>
>$$
>E[X + Y] = E[X] + E[Y]
>$$
>
>$$
>E[X_{1} + \dots+ X_{n}] = E[X_{1}] + \dots + E[X_{n}]
>$$
>
>$$
>E[a_{1}X_{1} + \dots+ a_{n}X_{n}] = a_{1}E[X_{1}] + \dots + a_{n}E[X_{n}]
>$$
>
>più in generale dai $a_{1}, a_{2}, \dots , a_{n} \in \mathbb{R}$
>
>>[!example]- Esempio
>>Lancio una dado 1000 volte, calcolare $E[X]$ dove $X = \#\text{volte che esce 5}$
>>
>>>**Metodo 1 (lento):***
>>>
>>>Notiamo che possiamo $X$ può essere descritta utilizzando la binomiale quindi $X = \text{Bin(1000, 1/6)}$:
>>>
>>>Utilizziamo la [[Introduzione - Variabili Aleatorie#Valore Atteso|definizione di valore atteso]] otteniamo che:
>>>
>>>$$
>>>E[X] = \sum^{1000}_{k=0}k \binom{1000}{k} \left( \frac{1}{6} \right) ^{k} \left( \frac{5}{6} \right)^{1000-k}
>>>$$
>>>
>>>Ma questo è un calcolo molto lungo
>>
>>>**Metodo 2:**
>>>L'idea è di semplificare i calcoli scomponendo la v.a. $X$ in 1000 variabile più semplici.
>>>
>>>Possiamo scomporla in $X_{1}, \dots,X_{1000}$  dove $X_{i}$ vale 1 se la i-esima prova vale 5, 0 altrimenti, in questo modo otteniamo:
>>>
>>>$$
>>>E[X] = \sum^{1000}_{i=1} E[X_{i}]
>>>$$
>>>
>>>**oss:** la v.a. $X_{i}$ assume il valore $1$ con probabilità $\frac{1}{6}$ e il valore $0$ con probabilità $\frac{5}{6}$ quindi il valore atteso è per $x_{i}$ è $E[x_{i}] = 1 \cdot \frac{1}{6} + 0 \frac{5}{6} = \frac{1}{6}$
>>>
>>>Quindi la sommatoria precedente sarà 
>>>$$
>>>E[X] = \sum^{1000}_{k=0} \frac{1}{6} = 1000 \cdot  \frac{1}{6}
>>>$$
>>
>>***Notiamo*** che il secondo metodo non è altro i procedimento con cui si ottiene la [[Variabile Aleatoria di Binomiale#^77219d|formula del valore atteso di una variabile binomiale]] $E[X] = np$
>

>[!warning] Prop. Prodotto
>Questo vale soltanto se sono **indipendenti:**
>$$
>E[XY] = E[X] \cdot  E[Y]
>$$

