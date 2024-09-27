---
type: Uni Note
class: 
academic year: 2023/2024
related: 
completed: false
created: 2024-09-24T17:18
updated: 2024-09-25T19:49
---


## Esercizi

>[!example] Example
>Ho un azienda con:
>- 10 informatici
>- 5 segretari
>- 20 operai
>
>In quanti modi posso scegliere una delegazioni di:
>- 3 informatica
>- 2 segretari
>- 6 operai
>
>**Risposta:**
>- Possiamo sceglie 3 informatici in $\binom{10}{3}$ modi diversi.
>- Possiamo sceglie 2 segretari in $\binom{5}{2}$ modi diversi.
>- Possiamo sceglie 6 operai in $\binom{20}{6}$ modi diversi.
>
>Quindi la delegazione può essere composta in $\binom{10}{3} \cdot \binom{5}{2} \cdot \binom{20}{6}$ modi diversi.

>[!example] Example
>10 amici devo formare due squadre da 5, in quanti modi diversi si può fare.
>
>**Risposta:**
>- Questa domanda può essere riscritta come in quanti modi diversi posso estrarre 5 persone da un gruppo di 10.
>- Quindi: $\binom{10}{5}$

>[!example] Example
>6 studenti devono essere divisi in due gruppi di 4 e 2 studenti, in quanti modi si può fare.
>
>**Risposta:**
>- Basta scegliere 4 studenti, quindi dobbiamo capire in quanti modi diversi possiamo estrarre 4 persone da un gruppo da 6.
>- Quindi $\binom{6}{4}$
>
>**oss:** $\binom{6}{4} = \binom{6}{2}$



>[!danger]
>Ogni volta che dobbiamo scegliere $k$ persone da un gruppo di $n = k \cdot 2$ persone senza altre informazioni aggiuntive allora il basta fare la metà delle scelte.
>
>Quindi se dobbiamo fare due squadre da 5 partendo da dieci persone allora il calcolo sarà:
>$$
>\frac{1}{2}\cdot \binom{10}{5}
>$$
>
>Invece se dobbiamo dividere 10 persone in 2 square ma una con una maglia rossa e l'altra con maglia blu allora il calcolo sarà:
>$$
> \binom{6}{4}
>$$

>[!example] Example
>Vedi esempio pulizia  da appunti prof (sembra utile)

## Coefficiente multi binomiale

Immaginiamo di avere $n$ oggetti distinti che vigliamo ripartire in $r$ scatole distinte ($s_{1},s_{2}, \dots, s_{r}$) in modo tale che $\forall i = 1-r$ nella scatola $S_{i}$ metto gli oggetti dove $n_{1}+n_{2}+\dots+n_{r} = n$

Quante sone le permutazioni possibili ?

**Risposta:** 

$$
\frac{n!}{n_{1}!\cdot n_{2}!\cdot \dots \cdot n_{r} } :=\binom{n}{n_{1}, n_{2}, \dots, n_{r}} \ \ \ \ \textcolor{orange}{}\text{(coefficente binomiale multiplo)}
$$

**Fai collegamento con esempio pulizia**


>[!example] 
>In quanti modi e possibile suddividere 10 persone in in 5 gruppi da 2?
>
>**Risposta:** 
>$$
>\binom{10}{2,2,2,2,2} = \frac{10!}{2!2!2!2!2!}
>$$
