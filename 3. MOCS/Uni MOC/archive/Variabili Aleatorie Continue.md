---
type: Uni Note
class: "[[Calcolo delle Probabilità (class)]]"
academic year: 2024/2025
related:
  - "[[Variabili Aleatorie]]"
  - "[[Variabile Aleatoria Discreta]]"
completed: false
created: 2024-11-30T11:48
updated: 2024-11-30T14:57
---
>[!abstract] Related
>- [[Variabili Aleatorie]]
>- [[Variabile Aleatoria Discreta]]
>- [[Calcolo delle Probabilità (class)]]

---
## Introduzione

A differenza delle variabili aleatorie discrete, che possono assumere solo un numero finito o numerabile di valori, le variabili aleatorie continue possono assumere un numero infinito di valori all'interno di un intervallo

>[!note] Definizione Variabile Aleatoria Continua
>
>Una variabile aleatoria $X:S \to R$  è detta ***continua*** se esiste una funzione $f:\mathbb{R}\to [0,+\infty]$ tale che:
>
>$$
>P(X \in A) = \underset{A}{\int} f(x) \, dx 
>$$
>
>La suddetta funzione $f$ è detta *funzione di densità*.

## Variabile Aleatoria Continua Uniforme

Una ***variabile aleatoria continua uniforme*** è un tipo specifico di variabile aleatoria continua in cui tutti i *valori all'interno di un certo intervallo* hanno la *stessa probabilità* di essere assunti.

>[!note] Notazione
>Variabile aleatoria continua uniforme sull'intervallo $[a,b]$
>$$
>X = \text{Unif}\big([a,b]\big)
>$$

>[!note] Definizione 
>Una v.a. continua $X$ è detta ***uniforme*** sull'intervallo $[a,b]$ se ha come funzione di densità:
>
>$$
>f(x) = \begin{cases}
> \frac{1}{b-a} & \text{se } x \in [a,b] \\ \\
>0 & \text{altrimenti}
>\end{cases}
>$$
>
>***Proprietà:***
>- La variabile assume valori soltanto nel intervallo $[a,b]$
>- La probabilità di densità è costante e uguale a $\frac{1}{b-a}$ per ogni $x$ nell'intervallo $[a,b]$

---
## Densità di Probabilità

>[!note] Densità di probabilità (sotto intervallo)
>
>La probabilità che la variabile assuma un valore in un intervallo $[c,d]$ all'interno di $[a,b]$ è data da:
>
>$$
>P\big(X \in [c,d]\big)=\int^{d}_{c} f(x) \, dx = \frac{d-c}{b-a}
>$$
>
>Per ogni $a≤c<d≤b$ 
>
>![[Pasted image 20241130135315.png|500]]
>
>>[!example]- Esempio
>>
>>Se consideriamo una variabile aleatoria continua uniforme $X$ definita sull'intervallo $[2, 5]$, la sua unzione di densità di probabilità sarà:
>>
>>$$
>>f(x) = 
>>\begin{cases} 
>>\frac{1}{5 - 2} = \frac{1}{3} & \text{se } 2 \leq x \leq 5 \\
>>0 & \text{altrimenti}
>>\end{cases}
>>$$
>>
>>In questo caso, la probabilità di trovare $X$ in un intervallo specifico, ad esempio $[3, 4]$, sarà:
>>
>>$$
>>P(3 \leq X \leq 4) = \int_{3}^{4} \frac{1}{3} \, dx = \frac{1}{3} \cdot (4 - 3) = \frac{1}{3}
>>$$
>>
>>***oss:*** usando la formula semplificata $P(c≤X≤d) = \frac{d-c}{b-a} = \frac{4-3}{5-2} = \frac{1}{3}$

##### Casi Particolari

>[!note] Densità di probabilità su intervallo parzialmente contenuto
>
>Data $X = \text{Unif}\big([a,b]\big)$
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
>Data $X = \text{Unif}\big([a,b]\big)$ e gli intervalli $[c,d]$ ed $[e,f]$
>
>La probabilità che $X$ assuma un valore in $[c,d]$ o in $[e,f]$ può essere rappresentata come:
>
>$$
>P(X \in [c,d] \cup [e,f])
>$$
>
>Se gli ***intervalli sono sovrapposti*** li consideriamo un intervallo solo, esempio:
>![[Pasted image 20241130135002.png|500]]
>
>$$
>P(X \in [c,d] \cup [e,f]) = P(X \in [c,f])
>$$
>
>Se gli ***intervalli non hanno elementi in comune*** allora:
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
## Valore Atteso e Varianza

>[!note] Valore Atteso (Aspettativa)
>L'aspettativa di una variabile aleatoria uniforme continua è data da: 
>$$
>E[X] = \frac{a+b}{2}
>$$

>[!note] Varianza
>
>La varianza di una variabile aleatoria uniforme continua è data da:
>
>$$
>\text{Var}(X) = \frac{(b-a)^{2}}{12}
>$$

---
## Proprietà
Sia $X = \text{Unif}\big([a,b]\big)$,

- $P\big( X \in [a,b] \big) = 1$
- $P\big( X \in [-\infty,+\infty] \big) = 1$


---
***Da Rivedere***

![[Pasted image 20241130132611.png|700]]
