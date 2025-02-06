---
type: Uni Note
class: "[[Calcolo delle Probabilità (class)]]"
academic year: 2024/2025
related:
  - "[[Variabili Aleatorie]]"
completed: false
created: 2024-12-09T11:58
updated: 2025-02-04T12:38
---

>[!abstract] Related
>- 

---
## Introduzione

È possibile avere delle variabili aleatorie diverse, con spazi campionari diversi ma che hanno la stessa funzione distribuzione, vediamo un esempio:

>***Caso 1:***
>
>Abbiamo un mazzo da 40 carte, estraiamo una carta e definiamo:
>
>$$
>X = \begin{cases}
>1 &\text{se estraggo Bastoni o Coppe}\\ \\
>0 &\text{altimenti}
>\end{cases}
>$$
>Come spazio campionario abbiamo il mazzo di carte e quindi esiti, quindi calcoliamo:
>
>$$
>P(X=1) = \frac{1}{2} \ \ \ \ \ \ \ \ \ P(X=0) = \frac{1}{2}
>$$

>***Caso 2:***
>
>Abbiamo una moneta, lanciamola e definiamo:
>
>$$
>Y = \begin{cases}
>1 &\text{se estraggo Testa (T)}\\ \\
>0 &\text{se esce Croce (C)}
>\end{cases}
>$$
>Come spazio campionario abbiamo $S = \{ T,C \}$, quindi calcoliamo:
>
>$$
>P(X=1) = \frac{1}{2} \ \ \ \ \ \ \ \ \ P(X=0) = \frac{1}{2}
>$$

Notiamo che X,Y sono v.a. distinte e anche con funzioni definite anche su spazi campionari diversi, nonostante questo assumono gli stessi valori con le stesse probabilità.

---
## Definizione

>[!note] Definizione
>
>Date v.a. $X:S \to \mathbb{R}$ e $Y:S' \to \mathbb{R}$, $X$ e $Y$ sono dette **identicamente distribuite** se:
>
>$$
>P(X \in A) = P(Y \in A)\ \ \ \forall A \subset \mathbb{R} 
>$$

>[!note] Prop. Discrete
>Siano $X$ e $Y$ v.a. discrete (anche con spazzi campionari diversi) allora:
>
>$$
>X \text{ e } Y \text{ sono } I.D. \iff p_{X} = p_{Y}
>$$
>
>>***oss:*** `P.I.` = Identicamente Distribuite
>
>>[!warning]- Dim
>>
>>Sappiamo che se $X$  è v.a. discreta che assume valori $\{x_{i}\}_{i\in I}​$ allora $P(X \in A)=P(X \in A \cap \{x_{i}​\}_{i\in I​})$ che è equivalente a:
>>
>>$$
>>P\left(\; \bigcup_{i:\; x_{i} \in A} \{X=x_{i}​\} \right) = \sum_{i:\; x_{i} \in A} P(X= x_{i}​) = \sum_{i:\; x_{i}\in A} p_{X}​(x_{i}​) = \sum_{X \in A}p_{X}
>>$$
>>
>>In conclusione quindi $P(X \in A) = \sum_{x \in A}\; p_{X}(x)$
>>
>>Ora definiamo $X$ e $Y$ due v.a. discrete e supponiamo che $p_{X} = p_{Y}$, allora per quanto appena visto possiamo dire che:
>>
>>$$
>>\textcolor{orange}{P(X \in A)} = \sum_{x \in A}p_{X}(x) \underset{p_{X}=p_{Y}}{=} \sum_{x \in A}p_{Y}(x) = \textcolor{orange}{P(Y \in A)}
>>$$
>>
>>Abbiamo provato quindi che due v.a. discrete $X$  e $Y$  con $p_{X} = p_{Y}$​ sono **identicamente distribuite** e si può provare anche il viceversa.

>[!note] Prop. Continue
>
>Siano $X$ e $Y$ v.a. continue (anche con spazi campionari diversi) chiamiamo $f_{X}$​ e $f_{Y}$​ le rispettive funzioni di densità di probabilità, allora:
>
>$$
>X \text{ e }Y\text{ sono } I.D. \iff f_{X} ​= f_{Y}​\ \ \text{(quasi ovunque)}
>$$
>
>>[!warning]- Dim
>>
>>
>>Siano $X$ e $Y$ due v.a. discrete e supponiamo che $f_{X} = f_{Y}$, allora:
>>
>>$$
>>\textcolor{orange}{P(X \in A)} = \int_{A} \frac{f_{X}}{x} \, dx  \underset{f_{X}=f_{Y}}{=} \int_{A} f_{Y}(x)  \, dx  = \textcolor{orange}{P(Y \in A)}
>>$$
>>
>>Abbiamo provato quindi che due v.a. discrete $X$ e $Y$  con $f_{X}​ = f_{Y}$​ sono **identicamente distribuite** e si può provare anche il viceversa.

---
## Teorema di De Moivre - Laplace

Fissiamo $p \in (0,1)$