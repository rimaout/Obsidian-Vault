---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2024-10-02T13:35
updated: 2024-11-08T11:11
---
[!abstract] Index
>1. 

>[!abstract] Related
>- 

---

##

>[!example] Esempio
>Estraggo 3 carte da un mezzo di 40 carte, senza rimpiazzo, qual'è la probabilità che a 1° carte e la 3° siano uguali.
>
>- $M$ mazzo di 40 carte
>- $S = \{ (a,b,c) \}: a,b,c \in M$
>- $E = \{ (a,b,c) \in S: a=c \}$
>
>$$
>P(E) = \frac{{ \lvert E \rvert }  }{{ \lvert S \rvert }  } = \frac{40 \cdot 40 \cdot 1}{40\cdot 40\cdot 40} = \frac{1}{40}
>$$

>[!example] Esercizio per casa 1

>[!example] Esercizio per casa 2

>[!example] Esercizio per casa 3

>[!example] Esercizio per casa 4

>[!example] Esercizio per casa 5
>Qual'è la probabilità di estrarre 2 carte di seme diverso da un mazzo di 40 carte:
>
>**Versione con rimpiazzo:**
>- $M = \text{mazzo 40 carte}$
>- $S = \{ (a,b): a,b \in M \}$
>- $E = \{ (a,b) \in S: a \text{ e } b \text{ hanno semi diversi}\}$
>
>**Versione con rimpiazzo:**
>$$
>P(E) = \frac{{ \lvert E \rvert }  }{{ \lvert S \rvert }  } = \frac{40 \cdot 30}{40\cdot 40}
>$$
>
>**Versione senza rimpiazzo:**
>$$
>P(E) = \frac{{ \lvert E \rvert }  }{{ \lvert S \rvert }  } = \frac{40 \cdot 30}{40\cdot 39}
>$$

>[!example] Esempio
>Consideriamo due persone. Quale è la probabilità che abbiamo compleanno?
>- $S = \{ (x_{1}, x_{2}): x_{1}, x_{2} \in \{ 1,2,\dots 365 \}\}$
>- $E = \{ (x_{1}, x_{2}) \in S: x_{1} = x_{2}\}$
>
>$$
>P(E) = \frac{{ \lvert E \rvert }  }{{ \lvert S \rvert }  } = \frac{365}{365^{2}} = \frac{1}{365}
>$$

>[!example] Esempio
>Prendendo 3 persone a caso, e dando per scontato che le nascite siano equi distribuite per tutto l'anno. Qual'è la probabilità che queste 3 persone siano nate lo stesso giorno.
>
>- $S = \{  \}$
>- $E = \{ (x_{1},x_{2},x_{3})\in S: \exists i \not= j, j\leq 3 \text{ e } x_{i} \}$
>
>$$
>P(e) = 1-P(E^{c}) = 1 - \frac{{ \lvert E^{c} \rvert }  }{{ \lvert S \rvert }  }
>$$

>[!warning] oss
>Con $n$ persone, per calcolare $P(E)$ procedo come sopra (usando il complementare)

>[!example] Esempio
>Comporre un gruppo di 5 persone scegliendo da un gruppo di 6 uomini e 9 donne, Qual'è la probabilità che si crei un gruppo composto da 2 uomini e 3 donne
>- $E = $
>- $S = $
>
>- ${ \lvert S \rvert } = \binom{15}{5}$
>- ${ \lvert E \rvert } = \binom{9}{2} \cdot \binom{9}{2}$
>  
>$$
>P(E) = \frac{{ \lvert E \rvert }  }{{ \lvert S \rvert }  } = \frac{\binom{9}{2} \cdot \binom{9}{2}}{\binom{15}{5} } = \frac{240}{1001}
>$$








