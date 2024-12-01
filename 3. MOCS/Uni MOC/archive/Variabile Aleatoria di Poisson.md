---
type: Uni Note
class: "[[Calcolo delle Probabilità (class)]]"
academic year: 2024/2025
related:
  - "[[Variabile Aleatoria di Binomiale]]"
  - "[[Variabili Aleatorie]]"
completed: false
created: 2024-11-30T11:10
updated: 2024-11-30T11:38
---
>[!abstract] Related
>- [[Variabile Aleatorie Congiunte]]
>- [[Variabili Aleatorie]]
>- [[Calcolo delle Probabilità (class)]]

---
## Variabile Aleatoria di Poisson

Una variabile aleatoria di Poisson è una variabile aleatoria che rappresenta il numero di eventi che si verificano in un intervallo di tempo o spazio fissato, dove gli eventi sono indipendenti e hanno una probabilità costante di verificarsi.

>[!note] Notazione
>Indichiamo una v.a di Poisson $X$ di parametro λ con:
>$$
>X = \text{Pois}(\lambda)
>$$
>
>Dove λ (lambda) indica: la media del numero di eventi che si verificano nell'intervallo di tempo o spazio fissato
>
>>***oss:*** La variabile aleatoria di Poisson può assumere soltanto valori interi non negativi (0, 1, 2, ...).

---
## Formule

>[!danger] Densità di Probabilità Discreta
>La probabilità di ottenere $k$ eventi è data dalla formula:
>
>$$
>P_{X}(k) = P(X=k) = \frac{\lambda^k \cdot e^{-\lambda}}{k!}
>$$
>
>**Dove:**
>- $P_{X}(k) \geq 0 \forall  k = 0,1,2, \dots$
>- $\sum^{\infty}_{k=0} P_{X}(k)=1$
>  
>>[!warning]- Dim (da fare)

>[!danger] Calcolo Valore Atteso
>$$
>E[X] = \lambda
>$$
>
>>[!warning]- Dim (da fare)

>[!danger] Varianza
>$$
>\text{Var}(X) = \lambda
>$$
>
>>[!warning]- Dim (da fare)

>[!example]- Esempio
>Supponiamo di avere una linea di produzione dove si verificano errori con una media di 2 errori all'ora ($\lambda = 2$). Sia $X$ la variabile aleatoria che rappresenta il numero di errori che si verificano in un'ora.
>
>Determinare:
>1. Probabilità di ottenere 0 errori
>2. Probabilità di ottenere 1 errore
>3. Probabilità di ottenere 2 errori
>4. Valore atteso di $X$
>5. Varianza di $X$
>
>**1. Probabilità di ottenere 0 errori:**
>$$
>P(X=0) = \frac{\lambda^0 \cdot e^{-\lambda}}{0!} = e^{-2} \approx 0,135
>$$
>
>**2. Probabilità di ottenere 1 errore:**
>$$
>P(X=1) = \frac{\lambda^1 \cdot e^{-\lambda}}{1!} = 2e^{-2} \approx 0,271
>$$
>
>**3. Probabilità di ottenere 2 errori:**
>$$
>P(X=2) = \frac{\lambda^2 \cdot e^{-\lambda}}{2!} = \frac{4}{2}e^{-2} \approx 0,271
>$$
>
>**4. Valore atteso di $X$:**
>$$
>E[X] = \lambda = 2
>$$
>
>**5. Varianza di $X$:**
>$$
>\text{Var}(X) = \lambda = 2
>$$

---
## Approssimazione di variabile di Binomiale con Poisson

Se $n$ è molto grande e $p$ è piccolo, la variabile aleatoria binomiale $\text{Bin}(n,p)$ può essere approssimata dalla variabile aleatoria di Poisson con parametro $\lambda = np$

$$
\text{Pois}(n \cdot p) \approx \text{Bin}(n,p) \iff \text{Pois}(\lambda) \approx \text{Bin}\left( n,\frac{\lambda}{n}​ \right)
$$

Questa approssimazione è nota come "*legge dei piccoli numeri*" e si basa sul fatto che quando $n$ è molto grande e $p$ è piccolo, la *probabilità di successo in una singola prova è molto piccola*, e quindi la variabile aleatoria binomiale può essere approssimata da una variabile aleatoria di Poisson.

>[!warning] Teorema: Legge dei Grandi Numeri
>Dato $n \in \{ 1,2,\dots \}$ si $P_{n} \in [0,1]$ tale che:
>$$
>\exists \lim_{ n \to \infty } n \cdot  P_{n} =: \lambda > 0
>$$
>
>Allora $X_{n}=\text{Bin}(n , P_{n})$ e $Z = \text{Pos}(\lambda)$ allora:
>$$
>\lim_{ n \to \infty } P(X_{n} = k ) = P(Z=k)\ \ \ \forall k \in \{ 0,1,2,\dots \} 
>$$
>
>Quindi per $n$ grande possiamo approssimare $P(X_{n} = k) \approx P(Z=K)$, quindi in alcune situazioni abbiamo che:
>$$
>\text{Bin}(n,p) \approx \text{Pois}(\lambda)
>$$
>
>Dove presi $n,\ p,\ \lambda$ abbiamo che:
>- $n\gg 1$ ($n$ molto più grande di 1)
>- $np \approx \lambda$ (quindi $p \approx \frac{y}{n}$)
>
>>***oss:*** Cosa si intende per $\text{Bin}(n,p) \approx \text{Pois}(\lambda)$?
>>
>>$$
>>P(X = k) \approx P(Z=k)\ \ \forall k = 0,1,2,\dots 
>>$$
>>
>>Dove $X= \text{Bin(n,p)}$ e $Z =\text{Pois}(\lambda)$.
>
>>[!warning]- Dim (da fare)

>[!example]- Esempio Astratto
>Prendiamo la pagina di un libro e consideriamo la probabilità che un carattere venga stampato in modo errato. 
>
>Quindi abbiamo una v.a. binomiale infatti un numero di prove $n$ e due esiti, successo se stampato male e insuccesso altrimenti.
>
>Notiamo che $n$ è il numero di caratteri ed è molto alto all’interno di una pagina, e $p$ possiamo assumerla piccola.
>
>Possiamo quindi assumere $\text{Bin}(n,p) \approx Poisson(\lambda)$ dove $\lambda=n\cdot p$

>[!example]- Esempio Concreto
>Supponiamo che il numero di errori tipografici per pagina sia approssimato da $\text{Pois}\left( \frac{1}{2} \right)$
>
>**Versione 1:**
>Trovare la probabilità che ci sia almeno un errore a pagina 20.
>
>Definiamo una v.a. aleatoria $Z$ tale che  $Z:=\text{numero di errori a pagina 20}$, abbiamo che:
>$$
>\begin{align*}
>&- \ \ \ Z = \text{Pois}(\lambda) \text{ con } \lambda=\frac{1}{2}\\
>&- \ \ \ P(z = k) = e^{-1/2} \cdot \left( \frac{1}{2} \right)^{k} \cdot \frac{1}{k!}
>\end{align*}
>$$
>
>Possiamo considerare il fatto che ci sia almeno un errore come l’evento complementare di non ci sono errori, quindi possiamo calcolare:
>$$
>P(Z\geq 1) = 1 - P(Z=0) = 1 - e^{-\frac{1}{2}} \cdot \left( \frac{1}{2} \right)^{0} \cdot  \frac{1}{0!} = 1 - e^{- \frac{1}{2} } \approx 0.393
>$$
>
>**Versione 2:**
>Trovare la probabilità che ci sia esattamente 4 errori a pagina 20.
>
>Dobbiamo quindi calcolare:
>$$
>P(Z=4) = e^{-\frac{1}{2}} \cdot  \left( \frac{1}{2} \right)^{4} \cdot  \frac{1}{4!} = \frac{1}{\sqrt{ e }} \cdot \frac{1}{16} \cdot \frac{1}{24} \approx 0.00158 
>$$
>
>**La Poisson approssima una binomiale** $\text{Pois}(\lambda) \approx \text{Bin}\left( n, \frac{\lambda}{n} \right)$
