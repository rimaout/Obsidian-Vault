---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2024-11-20T14:18
updated: 2024-11-27T12:37
---

>[!example] Lancio un dado 1000 volte calcolano senza usare formulari, $E[X]$ dati $X = \#\text{volte in cuiesce 5}$
>
>$X = \text{Bin}\left( n=1000,p=\frac{1}{6}  \right)$
>
>Sappiamo che: $E[X] = \sum_{k=0}^{1000}k P(X=k) = \sum^{1000}_{k=0} k \binom{1000}{k}p^{k}(1-p)^{1000} = \sum^{1000}_{k=0} \binom{1000}{k} \left( \frac{1}{6} \right)^{k}\left( \frac{5}{6} \right)^{1000-k}$
>
>Ma questo metodo è molto lungo e faticosa, possiamo usare questo altro metodo più breve:
>
>introduciamo 1000 variabile aleatorie $X_{1}, \dots, X_{i}$ con $i$ che va da 1 a 1000
>
>dove: 
>- $X_{i}$ se è 1 significa che al i-esimo lancio è uscito 5
>- $X_{i}$ se è 0 significa che al i-esimo lancio non è uscito 5
>
>$X = X_{1} + X_{2} + \dots + X_{1000}$
>
>$$
>E\left[  X \right] = \sum E[X_{i}] = n \cdot p = 1000 \cdot  \frac{1}{6}
>$$

>[!warning] prop
>
>$X = \text{Bin}(n,p) \implies E[X] = n\cdot p$
>
>>[!warning] Dim
>>ldjafhakjlhszkjlhjk
>>
>>



