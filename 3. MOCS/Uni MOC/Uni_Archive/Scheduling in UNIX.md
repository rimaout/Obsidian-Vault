---
type: Uni Note
class:
  - "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related: "[[Scheduling]]"
completed: true
created: 2024-11-06T19:33
updated: 2024-11-07T11:54
---
>[!abstract] Related
>- [[Scheduling]]
>- [[Sistemi Operativi 1 (class)]]

---
## Introduzione

In UNIX vengono utilizzati diversi algoritmi di scheduling insieme, nello specifico è combinata il concetto di priorità con l’algoritmo [[Algoritmi di Scheduling#Round Robin|Round Robin]]

>[!note] Caratteristiche
>- Un processo resta in esecuzione per un quanto (un secondo in unix) a meno che non termini o si blocchi.
>- Ci sono diverse code per ogni priorità e su ognuna si utilizza il Round-Robin
>- Ogni secondo vengono ricalcolate le priorità, quindi più uno resta in esecuzione più la sua priorità viene abbassata.
>- Le priorità iniziale vengono stabilite in base al tipo di processo:
>    - Swapper (alta), gestisce la memoria virtuale
>    - Controllo dispositivi I/O a blocchi (dischi)
>    - Gestione file
>    - Controllo dispositivi I/O a caratteri (tastiera)
>    - Processi Utente (bassa)

---
## Priorità

Per scegliere quale processo eseguire viene data una prioritaria ad ognuno ed ogni secondo viene aggiornata.

>[!note] Caratteristiche
>- Più il valore è basso più è alta la priorità di esecuzione
>- Formula sufficientemente semplice da avere un overhead basso (ovvero il calcolo non deve essere troppo dispendioso per la CPU) ma allo stesso tempo deve assicurare delle buone performance\

>[!danger] Formula
>
>$$
>P_{j}(i) = \text{Base}_{j} + \frac{\text{CPU}_{j}(i)}{2} + \text{nice}_{j}
>$$
>
>>**oss:** $\text{CPU}_{j}(i) = \frac{\text{CPU}_{j}(i-1)}{2}$
>
>Dove:
>- $\text{CPU}_{j}(i)$ indica quanto il processo $j$ ha usato il processore nell’intervallo $i$, usa **exponential averaging** dei tempi passati
>- Per i running, $\text{CPU}_{j}(i)$ viene incrementato di 1 ogni $\frac{1}{60}$ di secondo
>- $\text{base}_{j}$​ indica la categoria del processo vista prima
>- $\text{nice}_j​$, un processo può indicare questo valore "di cortesia" per auto-declassarsi e dare spazio ad altri processi (utilizzato solitamente in processi di sistema dove il S.O. sa che sone meno importanti)

---
## Esempio

In quest immagine i blocchi colorati rappresentano i processi in esecuzione, Priority rappresenta $P_{j}$, CPU count rappresenta $CPU_{j}$ e Time i quanti di tempo

![[Pasted image 20241107092942.png|400]]

>[!warning] Dati:
>- Hanno tutti li stesso valore di *nice* (0)
>- Hanno tutti li stesso valore di *base* (60)

>[!warning] Funzionamento:
>- Il processo **A** è to per primo e viene mandato in esecuzione, mentre gli altri non sono in esecuzione il loro valore di $\text{CPU}_{j}$​ non viene incrementato,​ mentre quello di **A** è aumentato di $\frac{1}{60}$.
>- Dopo un quanto (1 secondo) avviene un l’interrupt che arresta il processo **A**, il suo valore $\text{CPU}$ diventa $\frac{2}{60}$​ e nella priorità viene ridiviso per 2 e sommato a base quindi otteniamo 15+60=75 di priorità.
>- Viene quindi scelto **B** dato che è arrivato prima di **C** e ha priorità più bassa di A.
>- Vengono effettuati gli stessi passaggi di prima…

---
