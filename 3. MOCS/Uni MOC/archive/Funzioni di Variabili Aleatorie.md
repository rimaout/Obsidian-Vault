---
type: Uni Note
class: "[[Calcolo delle Probabilità (class)]]"
academic year: 2024/2025
related:
  - "[[Variabili Aleatorie]]"
completed: true
created: 2024-11-30T15:10
updated: 2026-01-31T13:32
---
>[!abstract] Related
>- [[Variabili Aleatorie]]
>- [[Calcolo delle Probabilità (class)]]

---
## Definizione 

Dati $(S, P)$ e $X:S\to \mathbb{R}$ 

Sia $f:\mathbb{R} \to \mathbb{R}$, Denoto con $f(X)$ la ***variabile aleatoria** $f \circ X$ ovvero:

$$
S \overset{X}{\to} \mathbb{R} \overset{f}{\to} \mathbb{R}
$$

>[!warning] Osservazioni
>- $f(X): S \to \mathbb{R}$ è una variabile aleatoria
>- $X: S \to \mathbb{R}$ assume i valori $\{ X_{i}: i \in I\}$
>- $f(X) = f \circ X:S\to \mathbb{R}$ assume i valori $\{ f(X_{i}: i \in I) \}$
  
>[!example] Esempio
>Lanciamo 10 volte una moneta e definiamo la v.a. $X$ come $X := \# \text{Teste Uscite}$
>- Vinco 2 euro per ogni testa
>- Perdo 1 euro per ogni croce
>
>Definiamo una v.a. $Y$ come $Y := \text{Guadagno/perdita dei 10 lanci}$
>
>Come si può notare $Y$ dipende strettamente da il valore di $X$ quindi è possibile definire $Y$ come $f(x)$, in particolare:
>
>$$
>Y = f(x) = 2X - 1(10-X) = 3X -10
>$$

---
## Calcolo del Valore Atteso

Per effettuare il calcolo del valore atteso di $f(X)$ ci sono due metodi, (il secondo è più semplice):

>[!note] 1° Metodo
>Chiamiamo i possibili valori di $f(X)$ come $\{ y_{j}: i \in J\}$ e calcoliamo:
>
>$$
>P(f(X) = y_{i}) \forall  j \in J 
>$$
>
>Per definizione del [[Introduzione - Variabili Aleatorie#Valore Atteso|valore atteso]] otteniamo che:
>
>$$
>E[f(X)] = \sum_{j} y_{j} \cdot  P(f(X) = y_{j})
>$$
>
>Consiste nel prendere tutti i valori possibili di $f(X)$, ovvero $y_{j}$, e moltiplicarli per la probabilità che la funzione assuma quel valore, ovvero $P(f(X) = y_{j})$. Infine, si sommano tutti questi prodotti per ottenere il valore atteso di $f(X)$.

>[!note] 2° Metodo (Teorema)
>
>Sia $X$ v.a. discreta che assume valori $\{ X_{i} \}_{i \in I}$ e sia $f: \mathbb{R} \to \mathbb{R}$, allora:
>$$
>E[f(X)] = \sum_{i\in I} f(X_{i}) \cdot P(X = X_{i})
>$$
>
>Consiste nel prendere tutti i valori che la variabile aleatoria $X$ può assumere ($X_{i}$), applicare la funzione $f$ a questi valori per ottenere $f(X_{i})$, e poi moltiplicare ogni valore di $f(X_{i})$ per la probabilità che la variabile aleatoria $X$ assuma quel valore ($P(X = X_{i})$). Infine, si sommano tutti questi prodotti per ottenere il valore atteso di $f(X)$.

>[!example] Esempio (molto utile)
>Data la v.a. $X$ che assume i valori $-1,0,3$ con rispettive probabilità 0.2, 0.5, 0.3.
>
>Calcolare $E((X-1)^{2})$
>
>>**Metodo 1**
>>
>>$$
>>Y = (X-1)^{2} \text{assume i valori} \begin{cases}
>>4 &\text{se }X=-1 \\
>>4 &\text{se }X=-3 \\
>>1 &\text{se }X=0
>>\end{cases}
>>$$
>>
>>- $P(Y=4) = P(X= -1) + P(X=3) = 0.2 + 0.3 = 0.5$
>>- $P(Y=1) = P(X=0) = 0.5$
>> 
>>$$
>>E[Y] = 4 \cdot 0.5 + 1 \cdot 0.5 = 2.5
>>$$
>
>>**Metodo 2:**
>>
>>$$
>>\begin{align*}
>>E[Y] &= f(-1) \cdot  P(X = -1) + f(0)\cdot P(X=0) + f(3)\cdot P(X=3)\\
>>&\ \ |\\
>>&= (-1-1)^{2} \cdot 0.2 + (0-1)^{2}\cdot 0.5 + (3-1)\cdot 0.3\\
>>&\ \ |\\
>>&= 0.8 + 0.5 + 1.2 = 2.5
>>\end{align*}
>>$$
