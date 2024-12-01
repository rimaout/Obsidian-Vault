---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2024-11-28T11:46
updated: 2024-11-30T15:18
---

>[!abstract] Related
>- 

---
## Definizione

Una variabile aleatoria congiunta è una variabile aleatoria che rappresenta il comportamento di due o più variabili aleatorie correlate.

>[!note] Notazione
>
>Siano $X$ e $Y$ due variabili aleatorie definite su uno stesso spazio campionario. Indichiamo con  $(X, Y)$ la variabile aleatoria congiunta ovvero una funzione che associa ad ogni punto dello spazio campionario un valore della coppia $X,Y$.

---
### Densità di Probailità Congiunta


Date due v.a $X$ e $Y$ definite sullo stesso spazio campionario ($X: S \to \mathbb{R}$ e $Y: S \to \mathbb{R}$) ed entrambe discrete dove:
- $X$ ha valori in $\{ x_{i} \}_{i \in I}$ 
- $Y$ ha valori in $\{ y _{j}\}_{j \in J}$

La densità di probabilità discreta disgiunta $P_{X,Y}$ è la funzione:

$$
P_{X \times Y}: \{ x_{i} \}_{i \in I} \times \{ y_{j} \}_{j \in J} \to  [0,1]
$$

Data da $P_{X, Y} (x_{i}, y_{j} )=P(X= x_{i}, Y = y_{j})$

>[!example]- Esempio 1
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

>[!example] Esempio 2 (fai esempio un solo dado)
>kjkjlhkjlhkj

>[!example] Esempio 3 (quello delle carte dato per casa per il 18 nov)
>asjdkfkjlsbkjbakj

>[!warning] Proprietà
>- $P_{X,Y}(x_{i}, y_{i}) \in [0,1]$
>- $\sum_{i\in I}\sum_{j \in J} P_{X,Y}(x_{i}, y_{j}) = 1$

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

>[!warning] Prop
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


>[!warning] Prop
>
>$$
>E[X_{1} + \dots+ x_{n}] = E[X_{1}] + \dots + E[X_{n}]
>$$
>
>$$
>E[a_{1}X_{1} + \dots+ a_{n}x_{n}] = a_{1}E[X_{1}] + \dots + a_{n}E[X_{n}]
>$$
>
>più in generale dai $a_{1}, a_{2}, \dots , a_{n} \in \mathbb{R}$
>
>esempio:
>![[Pasted image 20241128121857.png|600]]
