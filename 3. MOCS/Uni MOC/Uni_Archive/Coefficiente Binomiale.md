---
type: Uni Note
class:
  - "[[Calcolo delle Probabilità (class)]]"
academic year: 2023/2024
related:
  - "[[Calcolo Combinatorio]]"
completed: false
created: 2024-09-25T19:47
updated: 2024-09-25T19:50
---
>[!abstract] Index
>1. [[#Combinazioni Semplici]]
>2. [[#Combinazioni con Ripetizioni]]

>[!abstract] Related
>- [[Calcolo delle Probabilità (class)]]
>- [[Calcolo Combinatorio]]

---
## Combinazioni Semplici

>[!note] Definizione 
>Numero di sottoinsiemi di $k$ elementi **distinti** che si possono creare da un insieme di $n$ elementi distinti.
>
>$$
>C_{nk} = \binom{n}{k} = \frac{n!}{k(n-k)!}
>$$

>[!tip] Proprietà
>$$
>\binom{n}{k} = \binom{n}{n-k}
>$$

>[!example] Esempio 1
>In quanti modi si possono scegliere 3 persone da un gruppo di 90?
>
>>**oss:** $n=90$, $k=3$, ordine non conta, no ripetizioni.
>
>**Risposta:** 
>$$
>C_{nk} = \binom{90}{3} = \frac{90!}{3!(90-3)!} = \frac{90!}{3!\cdot 87!} = 117480
>$$

---

## Combinazioni con Ripetizioni

>[!note] Definition
>Numero di sottoinsiemi di $k$ elementi che si possono creare da un insieme di $n$ elementi distinti.
>
>$$
>C^{r}_{nk} = \binom{n+k-1}{k} = \frac{(n+k-1)!}{n!(n-1)!}
>$$

>[!example] Esempio 1
>In quanti modi posso estrarre 4 biglie da un cesto di 10 biglie (dopp ogni estrazione la biglia viene ri-inserita nel cesto)
>
>>**oss:** $n=10$, $k=4$, ordine non conta, ripetizioni.
>
>$$
>C^{r}_{nk} = \binom{10 + 4 -1}{4} = \frac{(10+4-1)!}{4!(10-1)!} = \frac{13!}{4!\cdot 9!}
>$$

---