---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2024-11-11T16:42
updated: 2024-11-11T18:21
---

## Variabile Aleatoria Geometrica


>[!note] Definition
>Una variabile aleatoria $X$ è detta **geometrice** di parametro $P$ sw assume i valori 1,2,3,... con probabilità:
>$$
>P(X=k) = (1-p)^{k-1}\cdot p\ \ \ \ \forall k = 1,2,3,\dots
>$$

>[!example] Esempio FOndamentale
>
>consideriamo una successione di proec indipendenti di tipo sucesso / insucesso dove p = probabilità di avere sucesso in una singola prova.
>
>$X =\#\text{provve effettuate fino al primo sucesso incluso}$.
>
>smlkanvdlòkn
>
>Infatti: 
>$$
>\begin{align*}
>P(x = k) &= P(I_{1} \cap I_{2} \cap \dots \cap I_{k-1} \cap I_{k})\\
>&= P(I_{1}) \cdot  P(I_{2}) \cdot \dots \cdot P(I_{k-1}) \cdot  P(I_{k})\\
>&=(1-p)^{k-1}\cdot  p
>\end{align*}
>$$

>[!warning] oss
>$$
>P(k = \infty ) = 0
>$$

>[!danger] Calcolo Valore Atteso
>$$
>E[X] = \frac{1}{p}
>$$

>[!danger] Varianza
>$$
>\text{Var}(X) = \frac{1-p}{p^{2}}
>$$


>[!example] Example:
>Lancio un dato fino a quando esce per la prima vota 6
>
>a) calcolare il valore atteso del numero di lanci effettuati
>b) Calcolare la probabilità di avere effettuato almeno 7 lanci.
>
>a)
>$Xa  = \# \text{ numero di laci effettuati per ottenere una faccia di valore 6}$
>$p = \frac{1}{6}\to \text{ probabilità che un lancio esca 6}$
>$EX = \frac{1}{p} = \frac{1}{\frac{1}{6}} = 6$
>
>b)
>$P(X\geq 7) =$

## Variabile Aleatoria Binomiale Negativa

Parametri $p \in (0,1)$ e $r \in \{  1,2,3,\dots \}$

$$
\text{Bin}^{-}(i, r)
$$
$$
X:= 
$$

>[!danger] Calcolo Valore Atteso
>$$
>E[X] = \frac{r}{p}
>$$

>[!danger] Varianza
>$$
>\text{Var}(X) = \frac{r(1-p)}{p^{2}}
>$$

>[!example] Esempio
>Un papà va al lunapark di 2 figli. Decide di giocare a seguente gioco:
>
>Si estrae una pallina a caso da un urna con 40 palline di cui una è dorata. Se si estrae quella dorata si vince un peluche.
>
>Qual è il valore atteso della spesa effettuata dal papà?
>
>$X:= \#\text{volte che il papà gioca}$
>$Y:= \text{spesa effettuata} = 1.5 \cdot X$ quindi $EY = 1.5 \cdot EX$
>$X = \text{Bin}^{-}\left( p = \frac{1}{40}, r = 2 \right)$ to $EX = \frac{r}{p} = \frac{2}{1/40} = 80$
>
>$E[Y] = 1.5 \cdot 80 = 120$ euro

>[!example] Esempio
>Calcolare il valore atteso e varianza del numero di volte che lancio un dado prima di avere 1 per quarto volte.
>
>$X:= \#\text{ lanci effetuati}$
>$X =\text{Bin}^{-}\left( p=\frac{1}{6}, r=4 \right)$

---

Ciao a te cara e buon inizio settimana a te e a tutti voi un abbraccio forte e un bacione a tutti e due e buon lavoro a te e a tutti i tuoi cari che ti vogliono bene e che sei una persona che non ha mai avuto un figlio ma non mi ricordo il nome di questo ragazzo che si chiama mamma. Di dove sono i miei nonni di fronte al mio papà che non si sa se si può fare la richiesta per la vaccinazione per i bimbi non si sa ancora niente per la macchina nuova non so che dirti non mi ha detto nulla e mi fa sapere quando posso passare per il saldo delle spese di condominio e di condominio e non c’è nulla da pagare e la macchina è già in garage io sono già qua fuori se ti va di fare.