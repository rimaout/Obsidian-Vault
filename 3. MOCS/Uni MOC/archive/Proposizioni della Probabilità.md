---
type: Uni Note
class:
  - "[[Calcolo delle Probabilità (class)]]"
academic year: 2024/2025
related: "[[Studio delle Probabilità]]"
completed: true
created: 2024-10-10T17:48
updated: 2024-10-15T14:15
---
>[!abstract] Index
>-  [[#1° Probabilità dell’evento impossibile]]
>-  [[#2° Additività finita]]
>- [[#3° Probabilità dell’evento complementare]]
>- [[#4° Monotonia della funzione di probabilità]]
>- [[#5° Somma probabilità di eventi non disgiunti]]

>[!abstract] Related
>- [[Studio delle Probabilità]]
>- [[Calcolo delle Probabilità (class)]]

---
### 1° Probabilità dell’evento impossibile

La probabilità dell’evento impossibile è uguale a 0.

$$
P(\emptyset ) = 0
$$

>[!warning]- Dimostrazione
>
>Utilizzando l’[[Definizioni e Assiomi della Probabilità#^3a8a3d|assioma 3 dalla funzione di probabilità]] 
>
>Prendiamo la successione $E_{1}​,E_{2}​,E_{3}​,...$ dove $E_{1} ​= \emptyset , E_{2}​ = \emptyset , E_{3}​ = \emptyset,...,$ quindi abbiamo che $\forall i \not= j$ l’intersezione $E_{i} \cap E_{j} = \emptyset$.
>
>Per l'assioma 3: $P\big(\bigcup_{i=1}^{\infty}E_{i} \big) = \sum_{i=1}^{\infty} P(E_{i})$, quindi $P(\emptyset) = \sum_{i=1}^{\infty} P(\emptyset)$ 
>
>Per l'assioma 1 sappiamo che: $P(\emptyset) = [0,1]$.
>
>Supponiamo che $P(\emptyset) \in (0,1]$ allora abbiamo che $\sum^{\infty}_{i=1}​P(\emptyset) = +\infty$ e quindi $P(\emptyset) \not= \sum^{\infty}_{i=1} ​P(\emptyset)$, per esclusione abbiamo che $P(\emptyset) = 0$ (altrimenti sarebbe $\infty$ che sappiamo essere impossibile perché max è 1)

---
### 2° Additività finita

Dati $n$ eventi a 2 a 2 [[Definizioni e Assiomi della Probabilità#^14f29a|incompatibili]] $E_{1}, E_{2}, \dots, E_{n}$ vale che:

$$
P \Big(   \bigcup_{i=1}^{n} E_{i} \Big) = \sum^{n}_{i=1} P \big( E_{i} \big)
$$

>[!example] Esempio
>- Domani piove con una probabilità 0.3
>- Domani c’è il sole con una probabilità 0.6
>- Domani nevica con una probabilità 0.1 
>
>Probabilità che piova o che nevichi = 0.3 + 0.1 = 0.4

>[!warning]- Dimostrazione
>Consideriamo la successione $F_{1}, F_{2}, \dots$ con: 
>
>$$
>F_{1} = E_{1}, F_{2} = E_{2}, \dots , F_{n}=E_{n}, F_{n+1} = \emptyset, F_{n+1} = \emptyset 
>$$
>
>Dato che la successione è fatta da eventi 2 a 2 [[Definizioni e Assiomi della Probabilità#^14f29a|incompatibili]] posso applicare il [[Definizioni e Assiomi della Probabilità#^3a8a3d|3° assioma]] e otteniamo:
>
>$$
>P \Big(\bigcup_{i=1}^{\infty}F_{i} \Big) = \sum_{i=1}^{\infty} P(F_{i})
>$$
>
>Che è equivalente a:
>$$
>P \Big(\bigcup_{i=1}^{\infty}F_{i} \Big) = P(E_{1}) + P(E_{2}) + \dots + P(E_{n}) + P(\emptyset ) + \dots 
>$$
>
>Per la [[#1° Probabilità dell’evento impossibile|probabilità dell'evento impossibile]] abbiamo che $P(\emptyset) = 0$ quindi tutti i $P(\emptyset)$ sono trascurabili, lasciando soltanto:
>$$
>P \Big(\bigcup_{i=1}^{\infty}F_{i} \Big) = P(E_{1}) + P(E_{2}) + \dots + P(E_{n})
>$$

---
## 3° Probabilità dell’evento complementare

Consideriamo un evento $E$ la probabilità del suo evento complementare $E^{c}$ sarà:

$$
P(E^{c}) = 1 - P(E) \ \ \ \ \forall E \subset S 
$$

>[!warning]- Dimostrazione
>$E$ e $E^{c}$ sono eventi [[Definizioni e Assiomi della Probabilità#^14f29a|incompatibili]], quindi per l’[[#2° Additività finita|additività finita]] abbiamo che:
>
>$$
>P \big( E \cup E^{c} \big) = P(E) + P(E^{c})
>$$
>
>Ma sappiamo che $E \cup E^{c} = S$, quindi possiamo dire che $P \big( E \cup E^{c} \big) = P(S) = 1$
>
>Allora:
>
>$$
>P(E) + P(E^{c}) = 1 \implies P(E^{c}) = 1 - P(E)
>$$

---
## 4° Monotonia della funzione di probabilità

Dati due eventi $F$ ed $E$ con $E \subset F$  vale che:
$$
P(F) \leq P(E)
$$


>[!warning]- Dimostrazione
>
>$F = E \cup (F \setminus E)$, quindi $E$ ed $F\setminus E$ sono disgiunti.
>
>Quindi, $P(F) = P(E) + P(F\setminus E)$ dato che per l’[[#1° Probabilità dell’evento impossibile|assioma 1]] $P(F\setminus E) \geq 0$ allora $P(E) + P(F \setminus E)\geq P(E)$
>
>![[Pasted image 20240930182639.png|350]]

---
## 5° Principio di Inclusione / Esclusione

$$
\begin{align*}
& \text{Due Eventi:}\ \ \ \ P(A \cup B) = P(A) + P(B) - P(A \cap B)\\ \\
& \text{Tre Eventi:}\ \ \ \ \ P(A \cup B \cup  C) = P(A) + P(B) + P(C) - P(A \cap B) - P(A \cap C) - P(B \cap C) + P(A \cap B \cap C)
\end{align*}
$$

>**Vedi:** [[Principio di Inclusione ed Esclusione]]

>[!example] Esempio
>
>Giulia ha 2 libri, L1 e L2. L'evento E corrisponde a "Le piace L1" mentre F a "Le piace L2". Sappiamo che:
>- $P(E) = 0,5$ (la probabilità che le piaccia L1 è del 50%)
>- $P(F) = 0,4$ (la probabilità che le piaccia L2 è del 40%)
>- $P(E \cap F) = 0,3$ (la probabilità che le piacciano entrambi è del 30%)
>
>Vogliamo calcolare la probabilità che non le piaccia alcun libro. Per farlo, calcoliamo prima la probabilità che le piaccia almeno un libro, che è l'unione degli eventi E e F:
>
>$$
>P(E \cup F) = P(E) + P(F) - P(E \cap F)
\geq 0,5 + 0,4 - 0,3
\geq 0,6
>$$
>
>L'evento complementare di "Le piace almeno un libro" è "Non le piace nessun libro". Quindi, la probabilità che non le piaccia alcun libro è:
>
>$$
>P((E \cup F)') = 1 - P(E \cup F)
>= 1 - 0,6
>= 0,4
>$$
>
>Quindi, la probabilità che non le piaccia alcun libro è del 40%.

---
