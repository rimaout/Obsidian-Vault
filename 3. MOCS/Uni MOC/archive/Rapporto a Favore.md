---
type: Uni Note
class:
  - "[[Calcolo delle Probabilità (class)]]"
academic year: 2024/2025
related: 
completed: true
created: 2024-10-19T14:53
updated: 2025-02-05T09:31
---
## Definizione 

Il Rapporto a Favore di un evento A è definito come il rapporto tra la probabilità che l'evento A si verifichi e la probabilità che l'evento A non si verifichi. In altre parole, è il rapporto tra la probabilità di successo e la probabilità di insuccesso.

Matematicamente, il rapporto a favore di un evento $A$ è definito come:

$$
\frac{P(A)}{P(A^{c})} = \frac{P(A)}{1-P(A)}
$$

---
## Esempi

>[!example] Esempio Partita
>Prendiamo una partita tra l'Italia e il Brasile, dove la vittoria dell'Italia è data 1 a 5. Con questo si intende che il rapporto a favore della vittoria dell'italia è $\frac{1}{5}$.
>
>In termini matematici L'evento $A = \text{\#l'italia vince la partita}$ ha come rapporto a favore:
>
>$$
>\frac{P(A)}{P(A^{c})} = \frac{1}{5}
>$$
>
>Conoscendo il rapporto a favore dell' evento $A$ possiamo calcolare la sua probabilità $P(A)$:
>
>$$
>\begin{align*}
>&\frac{P(A)}{P(A^{c})} = \frac{P(A)}{1-P(A)}\\
>&\frac{1}{5} = \frac{P(A)}{1-P(A)}\\
>&\frac{1}{5} \cdot  (1-P(A)) = P(A)\\
>&\frac{1}{5} - \frac{1}{5} P(A) = P(A)\\
>&\frac{1}{5} = P(A) + \frac{1}{5} P(A)\\
>&\frac{1}{{\cancel{ 5 }}} = \frac{6}{\cancel{ 5 }} P(A)\\
>&P(A) = \frac{1}{6}
>\end{align*}
>$$
>
>>**oss:** $P(A^{c}) = 1 - P(A) = \frac{5}{6}$

>[!example] Esempio Criminologia
>E' avvenuto un omicidio e i principale indagato è Mario. Dove $P(H)$ è la probabilità che Mario sia assassino basata  sulle attuali prove.
>
>Una nuova prova $E$ è stata trovata, possiamo ricalcolare la probabilità che mario sia l'assassino prendendo in considerazione la nuova prova in questo modo:
>
>$$
>P(H \vert E)
>$$
>
>Possiamo calcolare come la nuova prova $E$ abbia influenzato il rapporto a favore dell'evento $H$, facendo:
>
>$$
> \frac{P(H\vert E)}{P(H^{c} \vert E)}
>$$
>
>Mentre il rapporto a favore precedente alla nuova prova era:
>
>$$
> \frac{P(H)}{P(H^{c})}
>$$
>
>Inoltre per il teorema di Bayes sappiamo che:
>
>$$
>P(H \vert E) =\textcolor{orange}{\frac{P(H)\cdot P(E \vert H)}{P(E)}}
>$$
>
>E che:
>
>$$
>P(H^{c}\vert E) = \textcolor{JungleGreen}{\frac{P(H^{c}) \cdot  P(E\vert H^{c})}{P(E)}}
>$$
>
>Quindi è possibile calcolare il rapporto $frac{P(H\vert E)}{P(H^{c} \vert E)}$ come:
>$$
>\frac{P(H\vert E)}{P(H^{c} \vert E)} = \frac{\textcolor{orange}{\frac{P(H)\cdot P(E \vert H)}{P(E)}}}{\textcolor{JungleGreen}{\frac{P(H^{c}) \cdot  P(E\vert H^{c})}{P(E)}}} = \frac{P(H)}{P(H^{c})} \cdot \frac{P(H\vert E)}{P(H^{c} \vert E)}
>$$
>
>Che può essere visto come:
>
>$$
>\text{Vecchio Rapporto} \cdot  \frac{P(H\vert E)}{P(H^{c} \vert E)}
>$$
>
>Il nostro rapporto a favore quindi aumenta se $P(E\vert H)>P(E \vert H^{c})$ ovvero se il loro rapporto > 1. Aumenta se appunto l’ipotesi è vera piuttosto che quando è falsa.


![[Pasted image 20241016145931.png|500]]