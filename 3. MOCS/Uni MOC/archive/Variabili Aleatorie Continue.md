---
type: Uni Note
class: "[[Calcolo delle Probabilità (class)]]"
academic year: 2024/2025
related:
  - "[[Variabili Aleatorie]]"
  - "[[Variabile Aleatoria Discreta]]"
completed: true
created: 2024-11-30T11:48
updated: 2025-02-17T17:14
---
>[!abstract] Related
>- [[Variabili Aleatorie]]
>- [[Variabile Aleatoria Discreta]]
>- [[Calcolo delle Probabilità (class)]]

---
## Introduzione

A differenza delle variabili aleatorie discrete, che possono assumere solo un numero finito o numerabile di valori, le variabili aleatorie continue possono assumere un numero infinito di valori all'interno di un intervallo.

>[!note] Definizione Variabile Aleatoria Continua
>
>Una variabile aleatoria $X:S \to R$  è detta ***continua*** se esiste una funzione $f:\mathbb{R}\to [0,+\infty]$ tale che:
>
>$$
>P(X \in A) = \underset{A}{\int} f(x) \, dx 
>$$
>
>La suddetta funzione $f$ è detta *funzione di densità*.

---
#### Variabile aleatoria continua uniforme

Una ***variabile aleatoria continua uniforme*** è un tipo specifico di [[Variabili Aleatorie Continue|variabile aleatoria continua]] in cui tutti i *valori all'interno di un certo intervallo* hanno la *stessa probabilità* di essere assunti.

>[!note] Notazione
>Variabile aleatoria continua uniforme sull'intervallo $[a,b]$
>$$
>X = \text{Unif}\big([a,b]\big)
>$$
>
>**oss:** non c'è differenza tra $(a,b)$ e $[a,b]$

^6aeecb

---
## Funzione di Densità

>[!note] Funzione di Densità (V.a. Continua Uniforme)
>Una v.a. continua $X$ è detta ***uniforme*** sull'intervallo $[a,b]$ se ha come funzione di densità:
>
>$$
>f(x) = \begin{cases}
> \frac{1}{b-a} & \text{se } x \in [a,b] \\ \\
>0 & \text{altrimenti}
>\end{cases}
>$$
>
>**oss:** $f(X)\geq 0$

>[!note] Funzione di Densità (V.a. Continua NON Uniforme)
>Una v.a. continua $X$ ***NON uniforme*** sull'intervallo $[a,b]$ ha come funzione di densità $f(x)$ che può variare in modo non costante all'interno dell'intervallo. La funzione di densità deve soddisfare le seguenti condizioni:
>
>$$
>f(x) = \begin{cases}
> g(x) & \text{se } x \in [a,b] \\ \\
>0 & \text{altrimenti}
>\end{cases}
>$$
>
>Dove $g(x)$ è una funzione continua e positiva nell'intervallo $[a,b]$ e soddisfa la condizione di normalizzazione:
>
>$$
>\int_a^b g(x) \, dx = 1
>$$
>
>**oss:** $f(x)\geq 0$

---
## Densità di Probabilità

>[!note] Densità di probabilità (sotto intervallo)
>
>La probabilità che la v.a. continua definita su $[a,b]$ assuma un valore in un intervallo $[c,d]$ all'interno di $[a,b]$ è data da:
>
>$$
>P\big(X \in [c,d]\big)=\int^{d}_{c} f(x) \, dx
>$$
>
>Per ogni $a≤c<d≤b$ 
>
>![[Pasted image 20241130135315.png|500]]
>
>---
>
>>**oss:**
>>- $P\big( X \in [a,b] \big) = 1$
>>- $P\big( X \in [-\infty,+\infty] \big) = 1$

>[!tip] Formula semplificata per continue Uniformi 
>Data $X = \text{Unif}\big([a,b]\big)$
>
>$$
>P\big(X \in [c,d]\big)=\int^{d}_{c} f(x) \, dx = \frac{d-c}{b-a}
>$$

>[!example]- Esempio (uniforme)
>
>Se consideriamo una variabile aleatoria continua uniforme $X$ definita sull'intervallo $[2, 5]$, la sua unzione di densità di probabilità sarà:
>
>$$
>f(x) = 
>\begin{cases} 
>\frac{1}{5 - 2} = \frac{1}{3} & \text{se } 2 \leq x \leq 5 \\ \\
>0 & \text{altrimenti}
>\end{cases}
>$$
>
>In questo caso, la probabilità di trovare $X$ in un intervallo specifico, ad esempio $[3, 4]$, sarà:
>
>$$
>P(3 \leq X \leq 4) = \int_{3}^{4} \frac{1}{3} \, dx = \frac{1}{3} \cdot (4 - 3) = \frac{1}{3}
>$$
>
>***oss:*** usando la formula semplificata $P(c≤X≤d) = \frac{d-c}{b-a} = \frac{4-3}{5-2} = \frac{1}{3}$

>[!example]- Esempio (non uniforme)
>
>Calcolare $P(X>3)$ sapendo che $X$ v.a. continua con funzione di densità:
>
>$$
>f(x) = \begin{cases}
>cx^{2} &\text{se } x \in [1,5] \\ \\
>0 & \text{altrimenti}
>\end{cases}
>$$
>
>***Ricavare valore incognita:***
>
>Sappiamo che $1 = \int^{b}_{a} f(x) \, dx$ quindi:
>
>$$
>1 = \int^{5}_{1} f(x) \, dx = \int^{5}_{1} cx^{2} \, dx = c \cdot \int^{5}_{1} x^{2} \, dx = c \cdot \frac{x^{3}}{2} \Bigg|^{5}_{1} = c \cdot \Bigg(\frac{5^{3}}{3} - \frac{1^{3}}{3}\Bigg) = c \cdot \frac{124}{3}
>$$
>
>Quindi otteniamo che $1 = c \cdot \frac{123}{3}$, ovvero:
>$$
>c = \frac{3}{124}
>$$
>
>***Calcolare P(X>3):***
>
>**oss:** $P(X>3) = P\big(X \in (3, +\infty)\big) = P\big(X \in (3, 5]\big)$
>
>$$
> P\big(X \in (3, 5]\big) = \int^{5}_{3} c x^{2}  \, dx = c \cdot \frac{X^{3}}{3} \Bigg|^{5}_{3} = c \cdot \frac{5^{3}-3^{3}}{3} = c \cdot \frac{98}{3} = \frac{3}{124} \cdot \frac{98}{3} = \frac{98}{124}
>$$

^34982701

##### Casi Particolari

>[!note] Densità di probabilità su intervallo puntiforme
>
>Quando si considera la probabilità che una variabile aleatoria continua X assuma un valore in un singolo punto $x$​, si ha:
>
>$$
>P(X=x​)=0 \ \ \ \forall x \in \mathbb{R} 
>$$
>
>**Spiegazione "pratica":** In un intervallo chiuso, come ad esempio $[a,b]$, ci sono infiniti punti (valori) che la variabile aleatoria può assumere. Di conseguenza, la probabilità di ottenere un valore esatto (un singolo punto) è zero.

>[!note] Densità di probabilità su intervallo parzialmente contenuto
>
>Data v.a. $X$ continua su $[a,b]$
>
>Quando si calcola la probabilità che $X$ assuma un valore in un intervallo $[c,d$] che non è completamente contenuto nell'intervallo originale $[a,b]$, è necessario considerare solo la parte dell'intervallo $[c,d]$ che rientra in $[a,b]$.
>
>>[!example]- Esempio
>>Data $X = \text{Unif}\big([2,5]\big)$
>>
>>Per calcolare la probabilità che la variabile aleatoria continua uniforme $X$  assuma un valore nell'intervallo $[-2, 4]$, dobbiamo prima verificare se questo intervallo rientra nell'intervallo definito della variabile, che è $[2, 5]$.
>>
>>Poiché l'intervallo $[-2, 4]$ si sovrappone parzialmente con l'intervallo $[2, 5]$, dobbiamo considerare solo la parte dell'intervallo $[-2, 4]$ che rientra in $[2, 5]$. Quindi, l'intervallo di interesse diventa $[2, 4]$.
>>
>>***Calcolare la Probabilità***
>>
>>La probabilità che $X$ assuma un valore nell'intervallo $[2, 4]$ è data dall'integrale della funzione di densità di probabilità $f(x)$ su questo intervallo.
>>
>>La funzione di densità di probabilità per una variabile aleatoria continua uniforme definita su $[2, 5]$ è:
>>
>>$$
>>f(x) = 
>>\begin{cases} 
>>\frac{1}{5 - 2} = \frac{1}{3} & \text{se } 2 \leq x \leq 5 \\ \\
>>0 & \text{altrimenti}
>>\end{cases}
>>$$
>>
>>Quindi, calcoliamo la probabilità:
>>
>>$$
>>P(2 \leq X \leq 4) = \int_{2}^{4} f(x) \, dx = \int_{2}^{4} \frac{1}{3} \, dx = \frac{1}{3} \cdot (4 - 2) = \frac{1}{3} \cdot 2 = \frac{2}{3}
>>$$
>>
>>***oss:*** usando la formula semplificata $P(c≤X≤d) = \frac{d-c}{b-a} = \frac{4-2}{5-2} = \frac{2}{3}$

>[!note] Densità di probabilità su unione di intervalli
>
>Data v.a. $X$ continua su $[a,b]$ e gli intervalli $[c,d]$ ed $[e,f]$
>
>La probabilità che $X$ assuma un valore in $[c,d]$ o in $[e,f]$ può essere rappresentata come:
>
>$$
>P(X \in [c,d] \cup [e,f])
>$$
>
>---
>
>Se gli *intervalli sono sovrapposti* li consideriamo un intervallo solo, esempio:
>![[Pasted image 20241130135002.png|500]]
>
>$$
>P(X \in [c,d] \cup [e,f]) = P(X \in [c,f])
>$$
>
>---
>
>Se gli *intervalli non hanno elementi in comune* allora:
>![[Pasted image 20241130135118.png|500]]
>$$
>P(X \in [c,d] \cup [e,f]) = P(X \in [c,d]) + P(X \in [e,f])
>$$
>
>
>>[!example]- Esempio
>>Sia $X = \text{Unif}\big([2,8]\big)$, calcolare la probabilità che avvenga l'evento "$-3<X<4$ o $5\leq X <8$".
>>
>>Calcolare la probabilità di questo evento significa calcolare $P(X \in A)$ tale che $A = (-3,4) \cup [5,8)$
>>
>>Prima di tutto notiamo che l'intervallo l'intervallo $(-3,4)$ non è completamente contenuto da $[2,8]$ quindi prendiamo soltanto la parte che rientra in $[2,8]$ quindi il "nuovo" $C$ sarà $[2,4)$.
>>
>>Ora osserviamo che i due intervalli $[2,4)$ e $[5,8)$ non hanno elementi in comune quindi sappiamo che
>>
>>>[!note] Metodo Lungo
>>>$$
>>>P\big(X \in (2,4) \cup [5,8) \big) = P\big(X \in (2,4)\big) + P\big(X \in [5,8)\big)
>>>$$
>>>
>>>**Calcoliamo funzione di probabilità su $X$:**
>>>$$
>>>f(x) = \begin{cases}
>>> \frac{1}{8-2} = \textcolor{orange}{\frac{1}{6}} & \text{se } x \in [2,8] \\ \\
>>>0 & \text{altrimenti}
>>>\end{cases}
>>>$$
>>>
>>>**Quindi:**
>>>$$
>>>P\big(X \in (2,4)\big) = \int^{4}_{2} f(x) \, dx = \int^{4}_{2} \frac{1}{6} \, dx = \frac{1}{6}\cdot (4-2) = \frac{2}{6}
>>>$$
>>>
>>>$$
>>>P\big(X \in [5,8)\big) = \int^{8}_{5} f(x) \, dx = \int^{8}_{5} \frac{1}{6} \, dx = \frac{1}{6}\cdot (8-5) = \frac{3}{6}
>>>$$
>>>
>>>**Allora:**
>>>$$
>>>P\big(X \in (2,4) \cup [5,8) \big) = \frac{2}{6} + \frac{3}{6} = \frac{5}{6}
>>>$$
>>
>>>[!note] Metodo Veloce
>>>
>>>Metodo più veloce usando questa formula $P\big(X \in [c,d]\big) = \frac{d-c}{b-a}$ dove $X = \text{Unif}\big([a,b]\big)$
>>>
>>>$$
>>>P\big(X \in (2,4)\big) = \frac{4-1}{8-2} = \frac{2}{6}
>>>$$
>>>
>>>$$
>>>P\big(X \in [5,8)\big) = \frac{8-5}{8-2} = \frac{3}{6}
>>>$$

---
## Funzione di Distribuzione

La funzione di distribuzione (o ripartizione) è una funzione matematica che descrive la probabilità che una variabile aleatoria assuma valori inferiori o uguali a un certo valore.

**Vedi:** [[Introduzione - Variabili Aleatorie#Funzione di Distribuzione (o Ripartizione)|definizione generale di funzione di distribuzione]]

>[!note] Calcolo
>Data $X$ v.a. continue la funzione di distribuzione è calcolata facendo:
>
>$$
>F_{X}(b) = P(X<b) = \int_{-\infty }^{b} f(x) \, dx
>$$
>
>Dove:
>- $F_{X}(b)$ è la funzione di distribuzione di $X$
>- $f(x)$ è la funzione di densità di $X$

>[!warning] F(X) vs f(x)
>
>![[Pasted image 20241203124751.png|900]]

>[!example]- Esempio (uniforme)
>Calcolare la funzione di distribuzione $F(x)$ di $X = Unif\big( [-2,10] \big)$
>
>**Funzione di densità:**
>
>$$
>f(x) = \begin{cases}
>\frac{1}{12} & \text{se } -2\leq x \leq 10 \\ \\
>\ 0 & \text{altrimenti}
>\end{cases}
>$$
>
>Sappiamo che $F(x) = \int^{x}_{-\infty}  f(u)\, dx$, dobbiamo considerare tre casi per $F(x)$:
>
>$$
>\begin{align*}
>&\\
>&1. \ \ X < -2 \ \ \implies \ \ F(X) = \int^{x}_{-\infty} 0 \, du = 0\\ \\
>&2. \ \ -2\leq x \leq 10 \ \ \implies \ \ F(X) = \int^{x}_{-\infty} \frac{1}{12} \, du = \frac{x -(-2)}{12} = \frac{x+2}{12}\\ \\ 
>&3. \ \ X > 10 \ \ \implies \ \ F(X) = \int^{x}_{-\infty} f(u) \, du = \int^{10}_{-2} f(u) \, du = 1\\ \\
>\end{align*}
>$$
>
>Quindi:
>
>$$
>F(x) = \begin{cases}
>0 & \text{se } x < 2 \\ \\
>\frac{x+2}{12} & \text{se } -2\leq x \leq 10 \\ \\
>1 &\text{se } x > 10
>\end{cases}
>$$

>[!example]- Esempio (non uniforme)
>
>>**oss:** continuo di [[#^34982701|questo esempio]]
>
>Calcolare la funzione di distribuzione $F(x)$ di $X$ v.a. continua tale che:
>
>$$
>f(x) = \begin{cases}
>\frac{3}{124}x^{2} & \text{se } x \subset [1,5] \\ \\
>\ 0 & \text{altrimenti}
>\end{cases}
>$$
>
>Sappiamo che $F(x) = \int^{x}_{-\infty}  f(u)\, dx$, dobbiamo considerare tre casi per $F(x)$:
>
>$$
>\begin{align*}
>&\\
>&1. \ \ X < 1 \ \ \implies \ \ F(X) = \int^{x}_{-\infty} 0 \, du = 0\\ \\
>&2. \ \ 1\leq x \leq 5 \ \ \implies \ \ F(X) = \int^{x}_{1} \frac{3}{124}x^{2} \, du = \frac{\cancel{3}}{124} \cdot \frac{u^{3}}{\cancel{3}} \Bigg|^{x}_{1} = \frac{x^{3}-1}{124} \\ \\ 
>&3. \ \ X > 5 \ \ \implies \ \ F(X) = \int^{x}_{-\infty} f(u) \, du = \int^{5}_{1} f(u) \, du = 1\\ \\
>\end{align*}
>$$
>
>Quindi:
>
>$$
>F(x) = \begin{cases}
>0 & \text{se } x < 1 \\ \\
>\frac{x^{3}-1}{124} & \text{se } 1 \leq x \leq 5 \\ \\
>1 &\text{se } x > 5
>\end{cases}
>$$

---
## Valore Atteso

>[!note] Definizione
>Se $X$ è variabile aleatoria continua allora
>
>$$
>E[X] := \int^{+\infty }_{-\infty } x f(x) \, dx 
>$$
>
>***Formula semplificata continue uniformi:*** $E[x] = \frac{a+b}{2}$ (è al centro dell'intervallo)

>[!note] Valore atteso funzione di v.a.
>
>Sia $X$ v.a. continua con funzioni di densità $f$ e sia $g:\mathbb{R} \to \mathbb{R}$, allora:
>
>$$
>E[g(x)] = \int^{+\infty }_{+\infty } g(x)f(x) \, dx 
>$$

>[!tip] Proprietà
>Stesse delle variabili aleatorie discrete:
>
>1. $X$ v.a. continua e $a,b \in \mathbb{R}$ allora:
>   
>$$
>E[aX+b] = a\cdot E[X] + b
>$$
>
>2. $X$ v.a. continua tale che $X_{1}, \; \dots ,\;  X_{n}$ con $a_{1},\; \dots, \; a_{n}\in \mathbb{R}$ allora:
>
>$$
>E\left[ \sum^{n}_{i=2} a_{i} X_{i}\right] = \sum^{n}_{i=1} a_{i} E[X_{i}]
>$$

---
## Varianza, Deviazione e Co-Varianza

>[!note] Definizione Varianza
>Sia $X$ v.a. continua allora la varianza è (come le altre aleatorie):
>
>$$
>Var(X) = E \big[ (X-EX)^{2} \big]
>$$
>
>***Formula semplificata continue uniformi:*** $\text{Var}(X) = \frac{(b-a)^{2}}{12}$

>[!note] Definizione Co-Varianza
>Siano $X$ e $Y$  v.a. continue (come le altre aleatorie:
>
>$$
>\text{Cov}(X,Y) = E[(X-EX)(Y-EY)]
>$$