---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: true
created: 2024-11-30T11:24
updated: 2025-02-17T17:11
---
>[!abstract] Related
>- [[Variabile Aleatoria di Binomiale]]
>- [[Variabili Aleatorie]]
>- [[Calcolo delle Probabilità (class)]]

---
## Binomiale Negativa 

La variabile aleatoria binomiale negativa rappresenta il numero di prove necessarie per ottenere un certo numero di successi, dove ogni prova ha una probabilità costante di successo, e l'ultima prova deve essere un successo.

>[!note] Notazione
>Indichiamo una v.a. binomiale negativa $X$ di parametri $r,p$ con:
>$$
>X = \text{Bin}^{-}(r,p)
>$$
>
>Dove:
>- $r$ è il numero di successi desiderati
>- $p$ è la probabilità di successo in ogni prova

---
## Formule

>[!danger] Densità di Probabilità Discreta
>La probabilità di ottenere $k$ prove per ottenere $r$ successi dove l'ultima prova è sicuramente un successo è data dalla formula:
>
>$$
>P(X=k) = \binom{k-1}{r-1} \cdot p^r \cdot (1-p)^{k-r}
>$$
>

>[!danger] Valore Atteso
>$$
>E[X] = \frac{r}{p}
>$$
>

>[!danger] Varianza
>$$
>\text{Var}(X) = \frac{r(1-p)}{p^2}
>$$
>

---
## Esercizi

>[!example]- Esempio 1
>In questo gioco s estrae una pallina da urna di 40 paline di cui una è dorata, se si estrae quest'ultima si vince un peluche.  Vogliamo giocare finché non vinciamo 2 peluche.
>
>Calcolare il valore atteso della spesa sapendo che ogni estrazione di un pallina costa 1.5 euro.
>
>**Definiamo:**
>- $X = \text{Numero di volte che giochiamo}$
>- $Y = \text{Spesa effettuata} = 1.5 \cdot X$
>- $p = P(\text{Estrarre pallina dorata}) = \frac{1}{40}$
>
>Possiamo vedere $X$ come una variabile binomiale negativa infatti continuiamo a estrarre palline con probabilità $1/40$ fino a quando non otteniamo due successi, quindi:
>
>$$
>X = \text{Bin}^{-}\left( p = \frac{1}{40}, r=2 \right)
>$$
>
>**Valore atteso delle estrazione effettuate:**
>$$
>E[X] = \frac{r}{p} = \frac{2}{\frac{1}{40}} = 80
>$$
>
>**Valore atteso della spesa effettuata:**
>$$
>E[y] = E[X] \cdot  1.5 = 80 \cdot  1.5 = 120
>$$

>[!example]- Esempio 2 (utile)
>
>Due squadre di basket si sfidano ad una parità dove la prima ad arrivare a 4 match vinti allora vince la sfida.
>
>Sapendo che la squadra più forte ha una probabilità di $0.6$ di vincere ogni singola match, calcolare la probabilità che questa squadra vinca la sfida in esattamente $i$ incontri dove $i \in \{ 4,5,6,7 \}$.
>
>**Definiamo:**
>- $X = \#\text{match giocati}$
>
>$X$ non è altro che una v.a. binomiale negativa, infatti può essere vista come il numero di match giocati fino a quando la squadra più forte ottiene 4 vittorie con probabilità $0.6$, quindi:
>
>$$
>X= \text{Bin}^{-}(p=0.6 , r=4)
>$$
>
>Ora calcoliamo che la partita finisca in 4,5,6,7 match:
>
>$$
>\begin{align*}
>P(X = 4) &= \binom{4-1}{4-1} \cdot 0.6^{4} \cdot  (1-0.6)^{4-4}\\
>& \ \ |\\
>&= \binom{3}{3} \cdot 0.6^{4} \cdot (1-0.6)^{0} = 1 \cdot 0.6^{4} \cdot 1 = 0.1296\\ \\
>
>P(X = 5) &= \binom{5-1}{4-1} \cdot 0.6^{4} \cdot (1-0.6)^{5-4}\\
>& \ \ |\\
>&= \binom{4}{3} \cdot 0.6^{4} \cdot (1-0.6)^{1} = 4 \cdot 0.6^{4} \cdot 0.4 = 0.20736\\ \\
>
>P(X = 6) &= \binom{6-1}{4-1} \cdot 0.6^{4} \cdot (1-0.6)^{6-4}\\
>& \ \ |\\
>&= \binom{5}{3} \cdot 0.6^{4} \cdot (1-0.6)^{2} = 10 \cdot 0.6^{4} \cdot 0.4^{2} = 0.20736\\ \\
>
>P(X = 7) &= \binom{7-1}{4-1} \cdot 0.6^{4} \cdot (1-0.6)^{7-4}\\
>& \ \ |\\
>&= \binom{6}{3} \cdot 0.6^{4} \cdot (1-0.6)^{3} = 20 \cdot 0.6^{4} \cdot 0.4^{3} = 0.16588
>
>\end{align*}
>$$