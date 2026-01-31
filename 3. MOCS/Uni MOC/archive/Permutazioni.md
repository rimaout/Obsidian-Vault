---
type: Uni Note
class:
  - "[[Calcolo delle Probabilità (class)]]"
academic year: 2024/2025
related: []
completed: true
created: 2024-09-23T18:25
updated: 2026-01-31T13:32
---
>[!abstract] Related
>- [[Calcolo delle Probabilità (class)]]

---
## Permutazioni Semplici

>[!note] Definizione
>Numero di sequenze **ordinate** che si possono realizzare da $n$ elementi **distinti**.
>
>$$
>P_{n} = n!
>$$
>
>Dove $P_{n}$ indica il numero di permutazioni semplici di $n$ elementi.

>[!example] Esempio 1
>Le possibili permutazioni dell'insieme $\{ A,B,C \}$ sono $\{ ABC, ACB, BAC, BAC, CAB, CBA \}$

>[!example] Esempio 2
> Numero di anagrammi della parola MOUSE
>$$
>P_{5} = 5!
>$$

>[!example] Esempio 3
>Ci sono 120 studenti e 20 studentesse, in quanti modi posso scegliere un rappresentate e vice di sesso diverso?
>
>**Risposta:** $120! \cdot 20!$ oppure $20! \cdot 120!$

>[!example] Esempio 4
>In quanti modi diversi è possibile organizzare uno scaffale della libreria, tenendo conto che tutti i libri devono essere suddivisi in gruppi di categorie, quindi tutti i libri di matematica devono essere vicini , stessa cosa per quelli di chimica ...
>
>- 4 libri: di Matematica
>- 3 libri: di chimica
>- 2 romanzi
>
>**Risposta:**
>Dividiamo il problema in pezzi:
>- $M$ = combinazione matematica = $4!$
>- $C$ = combinazioni chimica = $3!$
>- $R$ = combinazioni romanzi = $2!$
>
>In quanto modi diversi posso ordinare $M, C, R$?
>- in $3!$
>
>Quindi $M \cdot C \cdot R \cdot 3!$ = $4! \cdot 3! \cdot 2! \cdot 3!$

---
## Permutazioni con Ripetizioni

>[!note] Definizione
>Numero di sequenze **ordinate** che si possono realizzare da $n$ elementi **non distinti**.
>
>$$
>P^{r}_{n} = \frac{n!}{R_{n_{1}}\cdot \dots \cdot R_{n_{k}}}
>$$
>
>dove $R$ sono gli elementi che si ripetono.

>[!example] Esempio 1
>Trovare il numero di anagrammi della parola MAMMA
>
>**Abbiamo che:**
>- $n=5 \ \ \ \  \ \ \to\ \ \text{numero di lettere.}$
>- $R_{A} = 2\ \ \ \to \ \ \text{numero di ripetizioni della lettera A.}$
>- $R_{M} = 3\ \ \to \ \ \text{numero di ripetizioni della lettera M.}$
>
>**Soluzione:**
>$$
>P^{r}_{n} = \frac{n!}{R_{A}! \cdot R_{M}!} = \frac{5!}{2! \cdot 3!}
>$$
