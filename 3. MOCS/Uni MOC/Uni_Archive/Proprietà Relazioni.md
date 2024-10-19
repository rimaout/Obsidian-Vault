---
created: 2023-11-13
type: Uni Note
class:
  - "[[Metodi matematici per l'informatica (class)]]"
academic year: 2023/2024
related:
  - "[[Relazioni]]"
  - "[[Relazioni d'ordine]]"
completed: false
updated: 2024-10-19T11:54
---
---
>[!abstract] Index
>1. [[#Riflessiva]]
>2. [[#Anti riflessiva]]
>3. [[#Simmetrica]]
>4. [[#Anti simmetrica]]
>5. [[#Transitiva]]
>6. [[#Chiusura Transitiva e Riflessiva]]
>7. [[#Esempio]]
>8. [[#Casi particolari]]

>[!abstract] Related
>- [[Relazioni]]
>-  [[Calcolo Differenziale (class)]]
>-  [[Metodi matematici per l'informatica (class)]]

---
## Riflessiva

Una relazione si dice riflessiva **quando ogni elemento dell'insieme considerato è in relazione con se stesso**.

$$
\forall a \in A \ \ \ (a,a)\in R
$$

---
## Anti-Riflessiva

Una relazione si dice anti-riflessiva quando **ogni elemento dell'insieme considerato non è in relazione con se-stesso**.

$$
\forall a \in A \ \ \ (a,a)\not \in R
$$

>**oss:** non esiste una funzione che è sia allo stesso tempo riflessiva ed anti-riflessiva.

---
## Simmetrica

Una relazione di dice anti simmetrica quando **per ogni coppia (a,b) esiste la coppia (b,a)**.

$$
\forall a,b \in A \ \ \ \ [(a,b)\in R] \implies[(b,a)\in R]
$$

---
## Anti-simmetrica

Una relazione si dice anti-simmetrica se:
- esiste una coppia (a,b) allora non deve esistere la coppia (b,a)
- esiste la coppia (a,b) e la coppia (b,a) allora a = b

$$ 
\forall a,b \in A \ \ \ \ [(a,b)\in R\ \ and \ \  \ (b,a)\in R]\implies a=b
$$

>[!warning] oss
>Può esistere una funzione che è allo stesso momento simmetrica ed anti-simmetrica, *esempio:* (1,1), (2,2), (3,3)

---
## Transitiva

Una relazione si dice transitiva quando **esiste la coppia (a,b) e la coppia (b,c) allora deve esistere la coppia (a,c)**.

$$
\forall a,b,c \in A\ \ \ \big[ (a,b) \in R\ \ and \ \ (b,c) \in R \big] \implies [(a,c) \in R]
$$

---
## Chiusure

>[!note] Chiusura Riflessiva
>

>[!warning] Chiusura Transitiva
>
>$$
>R \subseteq A \times A
>$$
>
>è la più piccola relazione transitiva che contiene R
>
>>**oss:** la chiusura transitiva di una relazione transitiva è la relazione stessa.

>[!note] Chiusura Simmetrica
>

>[!note] Chiusura Transitiva

- Sia R una relazione sull’insieme S
-  La **chiusura riflessiva** e **transitiva** di *R* è la più piccola relazione riflessiva e transitiva *R'* (un'altra relazione su S) che contiene R.

---
## Casi particolari

Può esistere una funzione che è sia simmetrica che anti simmetrica, *esempio:* (1,1), (2,2), (3,3)
