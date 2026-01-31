---
created: 2023-10-24T14:43
updated: 2026-01-31T13:32
related:
  - "[[Funzioni]]"
completed:
class:
  - "[[Metodi matematici per l'informatica (class)]]"
---
>[!abstract] Index
>1. [[#Proprietà]]

>[!abstract] Related
>- [[Funzioni]]
>- [[Matematica 0 (class)]] 

---
## Introduzione

Per poter effettuare l'operazioni di composizione $g \circ f$, il co-dominio di $f$ deve essere un sottoinsieme del dominio di $g$.

$$
Cod(f)⊆Dom(g)
$$

---
## Proprietà

>[!note] NON Commutativa
>In generale l'operazione di composizione di funzioni non gode della proprietà commutativa quindi:
>$$
> g \circ h \not = h \circ f
>$$
>
>Tuttavia, quando le funzioni sono inverse l'una dell'altra o quando sono funzioni identiche allora possiamo dire che $g \circ h = h \circ f$

>[!note] Composizione di Funzioni Iniettive 
>Se $f(x)$ e $g(x)$ sono [[Funzione Inniettiva, Surriettiva, Biettiva, Inversa#Funzione Inniettiva|funzioni iniettive]] sui rispettivi domini allora la funzione composta $g \circ f$ è una funzione **iniettiva** sul proprio dominio. 
>
>>Attenzione: in generale non vale il viceversa.

>[!note] Composizione di Funzioni Suriettive
>Se $f(x)$ e $g(x)$ sono [[Funzione Inniettiva, Surriettiva, Biettiva, Inversa#Funzione Surriettiva|funzioni suriettive]] sui rispettivi domini allora la funzione composta $g \circ f$ è una funzione **suriettiva** sul proprio dominio. 
>
>>Attenzione: in generale non vale il viceversa.

>[!note] Composizione di Funzioni Biettive
>Se $f(x)$ e $g(x)$ sono [[Funzione Inniettiva, Surriettiva, Biettiva, Inversa#Funzione Biettiva o Biunivoca|funzioni suriettive]] sui rispettivi domini allora la funzione composta $g \circ f$ è una funzione **biettive** sul proprio dominio. 
>
>>Attenzione: in generale non vale il viceversa.
