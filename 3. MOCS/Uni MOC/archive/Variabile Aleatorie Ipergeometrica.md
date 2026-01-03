---
type: Uni Note
class: "[[Calcolo delle Probabilità (class)]]"
academic year: 2024/2025
related:
  - "[[Variabili Aleatorie]]"
completed: true
created: 2024-11-30T11:40
updated: 2024-11-30T15:28
---
>[!abstract] Related
>- [[Variabili Aleatorie]]
>- [[Calcolo delle Probabilità (class)]]

---
## Variabile Aleatoria Ipergeometrica

Una variabile aleatoria ipergeometrica è una variabile aleatoria che rappresenta il numero di successi in una sequenza di prove senza sostituzione, dove ogni prova ha una probabilità di successo costante.

>[!note] Notazione
>Indichiamo una v.a. ipergeometrica $X$ di parametri $N, K, n$ con:
>$$
>X = \text{Hyp}(N, K, n)
>$$
>
>Dove:
>- $N$ è il numero totale di oggetti
>- $K$ è il numero di oggetti "successo"
>- $n$ è il numero di prove

---
## Formule

>[!danger] Densità di Probabilità Discreta
>
>La probabilità di ottenere $k$ successi in $n$ prove è data dalla formula:
>
>$$
>P(X=k) = \frac{\binom{K}{k} \cdot \binom{N-K}{n-k}}{\binom{N}{n}}
>$$

>[!danger] Calcolo Valore Atteso
>$$
>E[X] = \frac{n\cdot K}{N}
>$$

>[!danger] Varianza
>$$
>\text{Var}(X) = np\cdot (1-p) \cdot  \left( 1 - \frac{n-1}{N-2} \right)
>$$
>
>Dove $p = \frac{m}{N}$

---
## Esempi

>[!example]- Esempio 1
>Supponiamo di avere un'urna con 10 palline, di cui 4 sono rosse e 6 sono bianche. Estraiamo 3 palline senza sostituzione. Sia $X$ la variabile aleatoria che rappresenta il numero di palline rosse estratte.
>
>$$
>X = Hyp(N = 10, K = 4, n = 3)
>$$
>
>
>Determinare:
>1. Probabilità di ottenere 0 palline rosse
>2. Probabilità di ottenere 1 pallina rossa
>3. Probabilità di ottenere 2 palline rosse
>4. Probabilità di ottenere 3 palline rosse
>5. Valore atteso di $X$
>6. Varianza di $X$
>
>**1. Probabilità di ottenere 0 palline rosse:**
>
>$$
>P(X=0) = \frac{\binom{4}{0} \cdot \binom{6}{3}}{\binom{10}{3}} = \frac{1 \cdot 20}{120} = \frac{1}{6}
>$$
>
>**2. Probabilità di ottenere 1 pallina rossa:**
>
>$$
>P(X=1) = \frac{\binom{4}{1} \cdot \binom{6}{2}}{\binom{10}{3}} = \frac{4 \cdot 15}{120} = \frac{1}{2}
>$$
>
>**3. Probabilità di ottenere 2 palline rosse:**
>
>$$
>P(X=2) = \frac{\binom{4}{2} \cdot \binom{6}{1}}{\binom{10}{3}} = \frac{6 \cdot 6}{120} = \frac{1}{2}
>$$
>
>**4. Probabilità di ottenere 3 palline rosse:**
>
>$$
>P(X=3) = \frac{\binom{4}{3} \cdot \binom{6}{0}}{\binom{10}{3}} = \frac{4 \cdot 1}{120} = \frac{1}{30}
>$$
>
>**5. Valore atteso di $X$:**
>
>$$
>E[X] = \frac{3 \cdot 4}{10} = \frac{6}{5}
>$$
>
>**6. Varianza di $X$:**
>
>$$
>\text{Var}(X) = \frac{3 \cdot 4 \cdot 6 \cdot 7}{10^2 \cdot 9} = \frac{14}{25}
>$$