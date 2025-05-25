---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-05-12T14:19
updated: 2025-05-25T13:04
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
>![[Pasted image 20250525124853.png|750]]
>
>Un algoritmo backtracking in python che effettua dei print di queste soluzioni è:
>
>```python
>def es(S = []):
>	# se raggiunto 3° livello effettua print della soluzione
>	if len(S) == 3: 
>		print(S)
>		return
>
>	for c in ['G1', 'B1', 'B2']:
>		if c not in S:	
>			S.append(c)
>			es(S)
>			S.pop()
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
>
