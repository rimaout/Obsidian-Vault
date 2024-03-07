---
Created: 2023-11-13
Type: Uni Note
Class:
  - "[[Matematica Discreta (class)]]"
  - "[[Metodi matematici per l'informatica (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Relazioni]]"
  - "[[Relazioni d'ordine]]"
Completed: false
---
---
## Index
1. [[#Riflessiva]] {(1,2) (11) (22)}
2. [[#Anti riflessiva]] 
3. [[#Simmetrica]] 
4. [[#Anti simmetrica]] 
5. [[#Transitiva]]

- [[#Chiusura Transitiva e Riflessiva]] 
- [[#Esempio]] 
- [[#Casi particolari]]

$$\mathrm{Re}lazione\ \ R: A\to A$$

---
## Riflessiva
Una relazione si dice riflessiva quando ogni elemento dell'insieme considerato è in relazione con se stesso
$$\forall a \in A \ \ \ (a,a)\in R $$

---
## Anti riflessiva
Una relazione si dice quando ogni elemento dell'insieme considerato non è in relazione con se-stesso
$$\forall a \in A \ \ \ (a,a)\not \in R$$

**oss:** non esiste una funzione che è sia riflessiva che antiriflessiva

---
## Simmetrica
- Per ogni coppia (a,b) deve esistere la coppia (b,a)

$$ \forall a,b \in A \ \ \ \ [(a,b)\in R] \implies[(b,a)\in R]\ \ \ \ $$

---
## Anti simmetrica
- Se esiste una coppia (a,b) allora non deve esistere la coppia (b,a)
- Se esiste la coppia (a,b) e la coppia (b,a) allora a = b
$$ \forall a,b \in A \ \ \ \ [(a,b)\in R\ \ and \ \  \ (b,a)\in R]\implies a=b \ \ \ $$

**oss:** può esistere una funzione che è sia simmetrica che anti simmetrica, *esempio:* (1,1), (2,2), (3,3)

---
## Transitiva
- se esiste la coppia (a,b) e la coppia (b,c)  allora deve esistere la coppia (a,c)
$$\forall a,b,c \in A\ \ \ \big[ [(a,b)\in R]\ \ and\ \ [(b,c)\in R]\big] \implies [(a,c)\in R]$$

**Chiusura transitiva**
$$R \subseteq A \times A$$
è la più piccola relazione transitiva che contiene R

**oss:** la chiusura transitiva di una relazione transitiva è la relazione stessa

---
## Chiusura Transitiva e Riflessiva
- Sia R una relazione sull’insieme S
-  La **chiusura riflessiva** e **transitiva** di *R* è la più piccola relazione riflessiva e transitiva *R'* (un'altra relazione su S) che contiene R.
$$R\subseteq R'$$ 

---
## Esempio


---
## Casi particolari

Può esistere una funzione che è sia simmetrica che anti simmetrica, *esempio:* (1,1), (2,2), (3,3)

---