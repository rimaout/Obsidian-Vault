---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-05-12T14:19
updated: 2025-05-26T10:57
---
Il backtracking è una tecnica che utilizza il *brute forcing* per trovare tutte le soluzioni di un problema, in particolare è una tecnica di ricerca che esplora tutte le possibili configurazioni di un problema e da queste seleziona le soluzioni.

**Differenza con Programmazione dinamica:** Attraverso la [[Programmazione Dinamica|programmazione dinamica]] risolviamo *problemi di ottimizzazione*, il backtracking invece è solitamente utilizzato quando un problema ha diverse soluzioni ottime e le vogliamo trovare tutte.

**Albero delle soluzioni:** In particolare attraverso questa tecnica si ottiene un albero in cui sono presenti tutte le configurazioni e noi selezioniamo le sole foglie che rappresentano la soluzione. Può essere vista come una [[Visita in profondità (DFS) - Grafi|visita in profondità (DFS)]] ma dove l'albero viene generato allo stesso momento in cui lo si esplora.

>[!note] Esempio
>
>Abbiamo tre studenti due ragazzi ed una ragazza, ed abbiamo tre sedie l'obbiettivo è rappresentare tutte le possibili combinazioni.
>
>La soluzione può essere rappresentata sotto forma di albero, dove:
>- il livello 0 indica che nessuno è seduto
>- il livello 1 indica lo studente seduto nella 1° sedia
>- il livello 2 indica lo studente seduto nella 2° sedia
>- il livello 3 indica lo studente seduto nella 3° sedia
>
>![[Pasted image 20250525124853.png|600]]
>
>Un algoritmo backtracking in python che effettua dei print di queste soluzioni è:
>
>```python
>def es1(sol = []):
>	# se raggiunto 3° livello effettua print della soluzione
>	if len(sol) == 3: 
>		print(sol)
>		return
>
>	for c in ['G1', 'B1', 'B2']:
>		if c not in sol:
>			sol.append(c)
>			es(sol)
>			sol.pop()
>```
>**Output:**
>
>```
>['G1', 'B1', 'B2']
>['G1', 'B2', 'B1']
>['B1', 'G1', 'B2']
>['B1', 'B2', 'G1']
>['B2', 'G1', 'B1']
>['B2', 'B1', 'G1']
>```

## Funzione di taglio

La funzione di taglio permette di "tagliare" o escludere quelle configurazioni che sappiamo non porteranno a una soluzione valida, riducendo così il numero di possibilità da esplorare.

Questo avviene attraverso l'analisi di condizioni che, se non soddisfatte, indicano che una certa configurazione non è promettente per la ricerca di una soluzione.

>[!note] Esempio
>
>Modifichiamo l'esercizio precedente, aggiungendo la condizione che la studentessa può stare soltanto al 1° posto o al 3°.
>
>L'albero precedentemente utilizzato che esplorava tutte le possibili configurazioni non è più adatto per risolvere il problema, per questo inseriamo una funzione di tagligo che non permette alle studentessa di stare al secondo posto.
>
>![[Pasted image 20250525183016.png|600]]
>
>Un algoritmo backtracking in python che risolve il problema è:
>
>```python
>def es1T(sol = []):
>	if len(sol) == 3: 
>	    print(sol)
>	    return
>	
>	for c in ['G1', 'B1', 'B2']:	    
>	    
>	    # Funzione di taglio:
>	    if len(sol) == 1 and c == 'G1':
>	        continue
>	    
>	    if c not in sol:
>	        sol.append(c)
>	        es(sol)
>	        sol.pop()
>```

## Calcolo dei Costi

Prendiamo in considerazione questo problema risolvibile attraverso la tecnica del backtracking. Analizzeremo e confronteremo il costo di due algoritmi risolutivi: uno che non utilizza una funzione di taglio e uno che la utilizza.

>[!note] Teorema costo con funzione di taglio
>
>Si consideri un algoritmo di enumerazione basato sul backtraking dove l’albero di ricorsione ha altezza `h`, il costo di una foglia è `g(n)` e il costo di un nodo interno è `O(f(n))`.
>
>Se l’algoritmo gode della seguente proprietà: un nodo viene generato solo se ha la possibilità di portare ad una foglia da stampare.
>
>Allora la complessità dell’algoritmo è proporzionale al numero di cose da stampare `S(n)`, più precisamente la complessità dell’algoritmo è:
>
>$$
>O \big(S(n) \cdot  h \cdot  f (n) + S(n) \cdot  g(n)\big)
>$$
>
>Questo perché:
>- il costo totale dei nodi foglia sarà `O(S(n)·g(n))` (in quanto solo le foglie da enumerare verranno generate).
>- i nodi interni dell’albero che verranno effettivamente generati saranno `O(S(n)·h)` (in quanto ogni nodo interno generato apparterrà ad un cammino che parte dalla radice e arriva ad una delle `S(n)` foglie da enumerare).
 
>[!note] Problema
>
>Progettare un algoritmo che prende come parametro due interi `n` e `k`, con `0 <= k <= n`, e stampa tutte le stringhe binarie lunghe `n` che contengono al più `k` uni.
>
>***Ad esempio*** - per `n = 4` e `k = 2`, delle $2^{4} = 16$  stringhe lunghe `n` bisogna stampare le seguenti `11`:
>
>$$
>\begin{align*}
>&0000\ \ 0001\ \ 0010\ \ 0100\\ 
>&1000\ \ 0011\ \ 0101\ \ 1001\\ 
>&0110\ \ 1010\ \ 1100
>\end{align*}
>$$

##### Costo senza funzione di taglio

Vedremo un algoritmo che esplora tutte le possibili configurazione e poi stampa soltanto quelle che rispettano le condizioni del problema:

```python
def es2(n, k, sol=[]):
	if len(sol) == n:
		if sol.cont('1') <= k:
			print(''.join(sol))
		return

	sol.append('0'):
	es2(n, k, sol)
	sol.pop()
	sol.append('1'):
	es2(n, k, sol)
	sol.pop()
``` 

Questo algoritmo genera un albero delle soluzioni che contiene tutte le possibili configurazioni e poi sono selezionate le foglie che rispettano la condizione `sol.cont('1') <= k`.

![[Pasted image 20250525200221.png]]


>[!note] Calcolo del costo
>Come è facile intuire questo metodo non è particolarmente efficiente. Un buon algoritmo per questo problema dovrebbe avere una complessità proporzionale alle stringhe da stampare, ovvero `O(S(n,k)⋅n)` dove:
>- `S(n,k)` è il numero di stringe da stampare (ovvero che rispettano la condizione "lunghe `n` che contengono al più `k` uni")
>- `n` è il costo per dell'operazione `print` (il cui costo è proporzionale alla lunghezza della stringa in input)
>
>Quindi nel caso di questo problema, se poniamo `k=2`, un buon algoritmo per dovrebbe avere complessità polinomiale `O(n^3)`, visto che:
>
>$$
>S(n,k) = 1 + n + \binom{n}{2} = \Theta(n^{2}) 
>$$
>
>Mentre l'algoritmo da noi trovato ha complessità esponenziale $\Theta(2^{n} \cdot n)$, dato che visitiamo tutte le possibili soluzioni ($2^{n}$) su cui effettuiamo il controllo.

##### Costo con funzione di taglio

Adesso vediamo un altra soluzione al problema che utilizza una funzione di taglio per ridurre il costo computazionale:

```python
def es2T(n, k, c1=0, sol=[]):
	if len(sol) == n:
		print("".join(sol))
		return

	if c1 < k:               # c1 è utilizzato per contare il
		sol.append(1)        # numero di uni all'interno della stringa
		es2T(n,k,c1+1,sol)
		sol.pop()

	sol.append(0)
	es2T(n,k,c,sol)
	sol.pop()
```

In questo caso l'albero delle soluzione generato dell’algoritmo (con input `n=4` e `k=1`) contiene soltanto le configurazioni che portano ad una soluzione valida.

![[Pasted image 20250526095458.png]]

>***oss:*** nell'esempio i nodi in nero non vengono generati.

>[!note] Calcolo del Costo
>
>Per l'algoritmo codificato con la funzione `es2T(n,k)`. La proprietà di generare un nodo solo se questo può portare ad una delle `S(n,k)` foglie da stampare è rispettata.
>
>Dove:
>- `h = n` --> altezza albero (in questo caso lunghezza della stringa)
>- `g(n) = Θ(n)` --> costo delle foglie (in questo caso print)
>- `f(n) = O(1)` --> costo nodi intermedi 
> 
>Quindi la complessità dell'algoritmo è:
>
>$$
>S(n,k) \cdot  n \cdot O(1) + S(n,k) \cdot  \Theta(n) = \Theta(S(n,k) \cdot n)
>$$

g(n) = Θ(n) -> (costo foglie)
f(n) = Θ(1) -> (nodo intermedio)
h = n -> altezza albero (che è anche il numero di nodi per ramo nel caso peggiore)
S(n,k) = numero di foglie (è anche il numero di rami)

- (numero di foglie) x (costo foglia) + (numero di nodi intermedi) x (costo nodi intermedio)
- (S(n,k)) x (Θ(n)) + (S(n,k) x h ) x (Θ(1))