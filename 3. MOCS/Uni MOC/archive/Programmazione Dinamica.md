---
type: Uni Note
class: "[[Algoritmi 2 (class)]]"
academic year: 2024/2025
related: 
completed: false
created: 2025-04-27T17:15
updated: 2025-04-29T08:51
---
## Introduzione

La programmazione dinamica è una tecnica algoritmica che consiste nella memorizzazione delle soluzione di sotto problemi che si incontrano più volte durante il processo di risoluzione di un problema, in modo da non doverli ricomputare quando sono necessari in seguito.

Questa semplice ottimizzazione, in alcuni casi, può riduce le complessità temporali da esponenziali a polinomiali.

>[!note] Fibonacci
>
>Si può osservare questo fenomeno molto facilmente nel calcolo dei numeri di fibonacci, tramite l'algoritmo ricorsivo:
>
>```python
>def Fib(n):
>	if n <= 1: return 1
>	return Fib(n-1) + Fib(n-2)
>```
>
>Ad esempio per il calcolo di `fib(5)` verrano computati anche:
>
>![[Pasted image 20250428081954.png|850]]
>
>Visto che i sottoproblemi in cui viene scomposto il problema non sono disgiunti (**overlapping di sottoproblemi**) durante della scomposizione in sottoproblemi, stesse quantità vengono calcolate più volte da differenti chiamate ricorsive.
>
>È facile vedere che il costo computazionale questo algoritmo è rappresentato dalla seguente funzione:
>$$
>T(n) = T(n-1) + T(n-2) + \Theta(1)
>$$
>
>che viene risolta da:
>$$
>T(n) \geq 2T(n-2) + \Theta(1)
>$$
>
>E questa ricorrenza può essere facilmente risolta (ad esempio col metodo iterativo) ottendendo:
>$$
>T(n)\geq \Theta\left( 2^{\frac{n}{2}} \right)
>$$

## Memoizzazione

Una tecnica molto semplice prende il nome di **memoizzazione** e consiste nel memorizzare i risultati precedenti. Questo permette di ridurre il tempo di calcolo, al costo di un piccolo *incremento di occupazione di memoria*.

>[!note] Fibonacci
>
>Ad esempi un algoritmo iterativo, che utilizza la memoizzazione, per risolvere problema del calcolo dei numeri di fibonacci è:
>
>```python
>def Fib2(n):
>	F = [-1] * (n + 1)
>	F[0] = F[1] = 1
>	
>	for i in range(2, n + 1):
>		F[i] = F[i - 2] + F[i - 1]
>	
>	return F[n]
>```
>
>Grazie a questo algoritmo abbiamo ridorro il costo temporale a $\Theta(n)$, e il costo spaziale è sempre $\Theta(n)$.
>
>La complessità $\Theta(n)$ di spazio è a causa della lista da memorizzare ma in realtà dell'intera tabella basta conservare in memoria volta per volta solo gli ultimi due valori calcolati, riducendo il costo spaziale a $\Theta(1)$:
>
>```python
>def Fib3(n):
>	if n <= 1: return n
>
>	a = b = 1
>	for i in range(2, n + 1):
>		a, b = b, a + b
>
>	return b
>```

## Approccio Top-down e Botton-up

Nella versione ricorsiva del algoritmo per il calcolo dei numeri fibonacci, abbiamo utilizzato un approccio **top-down** al problema, ovvero 


**bottom-up** 