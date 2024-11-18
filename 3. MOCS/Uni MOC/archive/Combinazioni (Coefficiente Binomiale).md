---
type: Uni Note
class:
  - "[[Calcolo delle Probabilità (class)]]"
academic year: 2024/2025
related:
  - "[[Calcolo Combinatorio]]"
completed: true
created: 2024-09-25T19:47
updated: 2024-10-19T17:57
---
>[!abstract] Index
>1. [[#Combinazioni Semplici]]
>2. [[#Combinazioni con Ripetizioni]]

>[!abstract] Related
>- [[Calcolo Combinatorio]]
>- [[Calcolo delle Probabilità (class)]]

---
## Combinazioni Semplici

>[!note] Definizione 
>Numero di sottoinsiemi di $k$ elementi **distinti** che si possono creare da un insieme di $n$ elementi distinti.
>
>$$
>C_{nk} = \binom{n}{k} = \frac{n!}{k!(n-k)!}
>$$

>[!tip] Proprietà
>$$
>\binom{n}{k} = \binom{n}{n-k}
>$$

>[!example] Esempio
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

>[!note] Definizione
>Numero di sottoinsiemi di $k$ elementi che si possono creare da un insieme di $n$ elementi distinti.
>
>$$
>C^{r}_{nk} = \binom{n+k-1}{k} = \frac{(n+k-1)!}{k!(n-1)!}
>$$

>[!example] Esempio
>In quanti modi posso estrarre 4 biglie da un cesto di 10 biglie (dopp ogni estrazione la biglia viene ri-inserita nel cesto)
>
>>**oss:** $n=10$, $k=4$, ordine non conta, ripetizioni.
>
>$$
>C^{r}_{nk} = \binom{10 + 4 -1}{4} = \frac{(10+4-1)!}{4!(10-1)!} = \frac{13!}{4!\cdot 9!}
>$$

---
## Coefficiente Multinomiale

>[!note] Definizione
>l coefficiente multinomiale rappresenta il numero di modi in cui si possono disporre $\textcolor{orange}{n}$ oggetti distinti in m gruppi di dimensioni $\textcolor{orange}{k_{1}​,k_{2}​,...,k_{m}​}$.
>
>$$
>\binom{n}{k_{1}, k_{2}, \dots, k_{r}} = \frac{n!}{k_{1}!\cdot k_{2}!\cdot \dots \cdot k_{m} } 
>$$
>
>Dove:
>- $n$ è il numero totale di oggetti
>- $k_{1}, k_{2}​,...,k_{m}$​ sono le dimensioni dei gruppi
>- $m$ è il numero di gruppi

>[!example] Esempio
>Ad esempio, se si hanno 5 oggetti distinti e si vuole dividerli in 2 gruppi di 2 oggetti e 1 gruppo di 1 oggetto, il coefficiente multinomiale sarebbe:
>
>$\binom{5}{2,2,1} = \frac{5!}{2!\cdot 2!\cdot 1!} = 30$

>[!warning] oss
>In realtà il coefficiente multinomiale non è altre che un prodotto tra coefficienti binomiali.
>
>**Esempio:** 5 amici vogliono organizzare una festa e devono dividersi i compiti, 2 cucinano, 2 puliscono , 1 acquista il cibo. In quanti modi possono dividersi questi compiti?
>
>**Metodo 1 (multinomiale):** 
>$\binom{5}{2} \cdot \binom{3}{2} \cdot \binom{1}{1} =  \frac{5!}{2!3!} \cdot \frac{3!}{2!1!} \cdot \frac{1!}{1!1!} = \textcolor{orange}{\frac{5!}{2!2!1!}} = 30$ 
>
>**Metodo 2 (binomiale):** $\binom{5}{2,2,1} = \textcolor{orange}{\frac{5!}{2!\cdot 2!\cdot 1!}} = 30$
 
---
## Casi Particolari

>[!danger] Simmetria della scelta
>Ogni volta che dobbiamo scegliere $k$ persone da un gruppo di $n = 2k$ persone senza altre informazioni aggiuntive allora il basta fare la metà delle scelte.
>
>Il fenomeno si chiama "simmetria della scelta" e si verifica quando si deve scegliere un gruppo di oggetti da un insieme più grande, ma la scelta di un gruppo determina automaticamente l'altro gruppo.
>
>Quindi se dobbiamo fare due squadre da 5 partendo da dieci persone allora il calcolo sarà:
>$$
>\frac{1}{2}\cdot \binom{10}{5}
>$$
>
>Invece se dobbiamo dividere 10 persone in 2 square ma una con una maglia rossa e l'altra con maglia blu allora il calcolo sarà:
>$$
> \binom{6}{4}
>$$

---
## Esempi

>[!example] Esempio 1
>Ho un azienda con:
>- 10 informatici
>- 5 segretari
>- 20 operai
>
>In quanti modi posso scegliere una delegazioni di:
>- 3 informatica
>- 2 segretari
>- 6 operai
>
>**Risposta:**
>- Possiamo sceglie 3 informatici in $\binom{10}{3}$ modi diversi.
>- Possiamo sceglie 2 segretari in $\binom{5}{2}$ modi diversi.
>- Possiamo sceglie 6 operai in $\binom{20}{6}$ modi diversi.
>
>Quindi la delegazione può essere composta in $\binom{10}{3} \cdot \binom{5}{2} \cdot \binom{20}{6}$ modi diversi.

>[!example] Esempio 2
>In quanti modi e possibile suddividere 10 persone in in 5 gruppi da 2?
>
>**Risposta:** 
>$$
>\binom{10}{2,2,2,2,2} = \frac{10!}{2!2!2!2!2!}
>$$

>[!example] Esempio 3
>10 amici devo formare due squadre da 5, in quanti modi diversi si può fare.
>
>**Risposta:**
>- Questa domanda può essere riscritta come in quanti modi diversi posso estrarre 5 persone da un gruppo di 10.
>- Quindi: $\binom{10}{5}$

>[!example] Esempio 4
>6 studenti devono essere divisi in due gruppi di 4 e 2 studenti, in quanti modi si può fare.
>
>**Risposta:**
>- Basta scegliere 4 studenti, quindi dobbiamo capire in quanti modi diversi possiamo estrarre 4 persone da un gruppo da 6.
>- Quindi $\binom{6}{4}$
>
>**oss:** $\binom{6}{4} = \binom{6}{2}$
