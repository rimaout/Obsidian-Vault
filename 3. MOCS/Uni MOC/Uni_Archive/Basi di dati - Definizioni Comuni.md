---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2024-10-24T18:06
updated: 2024-10-24T18:31
---
>[!abstract] Index
>1. [[#Schema di relazione]]
>2. [[#Tupla]]
>3. [[#Istanza di Relazione]]

>[!abstract] Related
>- 

---

## Schema di relazione

Uno schema di relazione $R$ è un insieme di attributi $\{A_{1},…,A_{n}​\}$

>[!example] Esempio
>
>$$
>R=A_{1}​,…,A_{n}
>$$
>
>Dove:
>- $R$ rappresenta lo schema di relazione (insieme di attributi)
>- $A_{i}$ rappresenta il singolo attributo in posizione $i$

>[!warning] Notazione
>- Le prime lettere dell’alfabeto denotano singoli attributi
>- Le ultime lettere denotano insiemi di attributi
>- Se $X$ ed $Y$ sono insiemi di attributi allora $XY$ è usato per rappresentare denota $X∪Y$

---
## Tupla

Dato uno schema di relazione $R$

Dato uno schema di relazione $R$, una **tupla** $t$ su $R$ è una funzione che associa ad ogni attributo $A$ in $R$ un valore $t[A]$ nel dominio di $A$.

>**Proprietà:** Se $X$ è un sottoinsieme di $R$ e $t_{1}​,t_{2}$​ sono due tuple su $R$, $t_{1}$ e $t_{2}$​ coincidono su $X$ se $\forall A \in X$ abbiamo che $t_{1}[A] = t_{2}[A])$

---
## Istanza di Relazione

Dato uno schema di relazione $R$ una istanza di $R$ è un insieme di tuple su $R$

