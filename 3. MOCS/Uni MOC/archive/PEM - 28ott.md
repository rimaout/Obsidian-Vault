---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2025-10-28T17:17
updated: 2025-10-29T14:36
---
## Amdhal's Law

La legge di Amdhal è importante perché ci permette di trovare il limite asintotico dell'o speedup che possiamo ottenere.

$$
\lim_{ p \to \infty } S(p) = \frac{1}{1-\alpha}
$$
>[!example] Esempi
>
>Se il 60% dell'applicativo può essere paralizzato ($\alpha = 0.6$) significa che lo speed up massimo ottenibile è 2.5
>
>Se il 80% dell'applicativo può essere paralizzato ($\alpha = 0.8$) significa che lo speed up massimo ottenibile è 5
>
>Per avere uno speed up di 100000 dobbiamo avere $\alpha = 0.99999$.

![[Pasted image 20251028172632.png|600]]

## Gustafson’s Law

$$
S(n,p) = (1-\alpha) + \alpha p
$$

**Problemi**
 AUmentari il numero di processi non è sempre una buoba cosa...

Casa sono i thread? I ad esempio un processore può avere 8 core e 16 thread, questo significa che ogni core ha due contesti di memoria, in mo tale da contenere le informazione di due processori, queste permette di poter eseguire due processi su uno stesso processore senza thread di troppo le prestazioni, per questo a volte il numero di thread è il doppio del numero di core.

## Scatter

é una collettiva, ovvero un operazione che deve essere chiamata da tutte i processi.

La **scatter** normale "spreca" dello spazio, dato che per il nodo zero duplica l'informazione, per questo possiamo utilizzare **Scatter – In Place**


## Gather 

## Matrici Dinamiche allocate du più righe

L'unico modo per fare questo corettamente è fare una reduce per ogni riga, ma non è molto efficiente fato che è sempre conveniente raggruppare le send.

Quindi il modo migliore per effetuare una reduce su una matrice allocata dinamicamente in questo modo, è linearizarla ovvero allocare un array che contiene un numero di elementi pari al numero di righe per il numero di colonne.

## MPI_Sencrecv

Fa una send bloccante e una recive bloccante che è molto meglio di fare due chiamate bloccanti singolarmente.

