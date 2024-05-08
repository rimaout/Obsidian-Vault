---
Created: 2024-04-11
Type: Uni Note
Class:
  - "[[Introduzione agli Algoritmi (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Algoritmi di Ordinamento]]"
Completed: false
---
---

>[!info] Index
>1. [[#Introduzione]]
>2. [[#Funzionamento Generale]]
>3. [[#Implementazione Base]]
>4. [[#Versione in loco]]
>5. [[#Partition]]
>6. [[#Costo Temporale]]

>[!info] Related
>- [[Introduzione agli Algoritmi (class)]]
>- [[Algoritmi di Ordinamento]]

---
## Introduzione
L’algoritmo **quicksort** (ordinamento veloce) è un algoritmo ricorsivo che adotta una tecnica algoritmica detta [[Divide et Impera]]. 

Nonostante il costo nel caso peggiore sia $\Theta(n)$ (ovvero costo $O(n)$) è spesso la soluzione migliore per grandi valori di $n$ perché:
- Ha un tempo di esecuzione atteso di $O(n \log n)$
- I fattori costanti nascosti sono molto piccoli
- permette ordinamento "in loco"

>[!info]
>Riunisce i vantaggi del Selection sort (ordinamento in loco) e del Merge sort (ridotto tempo di esecuzione). Ha però lo svantaggio dell’elevato costo computazionale nel caso peggiore.

---
## Funzionamento Generale

>[!info] Funzionamento Generale
>L’approccio dell’algoritmo Quick Sort è il seguente:
>- **Divide:** Si seleziona un pivot posizionato in modo da ottenere due sotto sequenze: 
>	- Elementi minori o uguali al pivot, 
>	- Elementi maggiori al pivot
>- **Impera:**  Le due sotto sequenza vengono ordinate ricorsivamente
>- **Passo base:** La ricorsione procede fino a quando le sotto sequenze sono costituite da un solo elemento che è ovviamente ordinato.
>- **Combina:** non occorre.
>
>![[Pasted image 20240425192009.png|500]]

---
## Implementazione Base

>[!info] Codice
>```python
>def QuickSort(A):
>    # Se la lista è vuota o ha un solo elemento, è già ordinata
>    if len(A)<=1: return A  
>    
>    pivot = A[0]  # Sceglie il primo elemento come pivot
>    left, middle, right = [], [], []  # Crea tre liste vuote
>
>    for x in A:  # Per ogni elemento in A
>    
>        # Se è minore del pivot, va a sinistra
>        if x < pivot: left.append(x) 
>         
>        # Se è uguale al pivot, va al centro
>        elif x == pivot: middle.append(x)  
>        
>        # Se è maggiore del pivot, va a destra
>        else: right.append(x)  
>
>    # Ordina left e right, e le concatena con middle
>    return QuickSort(left) + middle + QuickSort(right)
>```

>[!danger] Non è una soluzione perfetta perché non è in loco e non sceglie il pivot 

>[!warning] Costo Temporale
>
>$$
>T(n) = \begin{cases}
>T(k) + T(n - \vert \text{middle} \vert - k) + \Theta(n) &\text{se } n\geq 2 \\
>\Theta(1) &\text{se }n<2
>\end{cases}
>$$
>
>dove $k$ è $0<k<n-\mid \text{middle}\mid$

>[!warning] Costo spaziale
>
>$$
>S(n) = O(n^{2})
>$$
>
>Alto costo spaziale dovuto alla creazione di liste di appoggio
	
---
## Versione in loco

>[!info] Codice
>
>```python
>def QuickSort(A, low ,high):
>    if low < high:  # Se la porzione da ordinare ha più di un elemento
>        
>        # Riorganizza la porzione e ottiene l'indice del 
>        p = Partition(A, low, high)  pivot
>        
>        # Ordina la porzione a sinistra del pivot
>        QuickSort(A, low, p-1)  
>        
>        # Ordina la porzione a destra del pivot
>        QuickSort(A, p, high)  
>```

>[!warning] Funzionamento
>1. Prende tre parametri: 
>	- Una lista `A` da ordinare
>	- Due indici `low` e `high` indicano l'inizio e la fine della porzione di `A` da ordinare
>2. Se `low` è minore di `high`, chiama una funzione `Partition` (non mostrata qui) che riorganizza la porzione di `A` da `low` a `high` in modo che tutti gli elementi minori di un certo pivot vengano prima del pivot e tutti gli elementi maggiori vengano dopo. La funzione `Partition` restituisce l'indice del pivot.
>3. Chiama ricorsivamente `QuickSort` su due porzioni di `A`: da `low` a `p-1` e da `p` a `high`. Questo ordina le due porzioni di `A` da entrambi i lati del pivot.

>[!danger] Costo Temporale
>$$
>T(n) = \begin{cases}
>T(k) + T(n - 1 - k) + \Theta(n) &\text{se } n\geq 2 \\
>\Theta(1) &\text{se }n<2
>\end{cases}
>$$
>dove $k$ è $0<k<n$
>
>**Leggi [[#Costo Temporale]] per approfondire i costi temporali del quicksort**

>[!danger] Costo Spaziale
>Ha un costo spaziale costante, ovvero O(1), perché non utilizza spazio di memoria aggiuntivo proporzionale alla dimensione dell'input.
>
>Infatti modifica "in loco" la lista originale ovvero esegue le modifiche direttamente sulla struttura dati di input, senza creare nuove copie o utilizzare spazio di memoria aggiuntivo significativo.

### Partition

>[!info] Codice 
>```python
>def Partition(A, low, high):
>    pivot = A[low]
>    pivot_index = low + 1
>
>    # Scambia gli elementi che sono minori del pivot
>    for current_index in range(low + 1, high + 1):
>        if A[current_index] < pivot:
>            A[current_index], A[pivot_index] = A[pivot_index], A[current_index]
>            pivot_index += 1
>
>    # Posiziona il pivot al suo posto definitivo
>    A[low], A[pivot_index - 1] = A[pivot_index - 1], A[low]
>
>    return pivot_index - 1
>```

>[!warning] Funzionamento
>La funzione `Partition` è una componente chiave dell'algoritmo di ordinamento QuickSort. Prende in input un array `A` e due indici, `low` e `high`, e riorganizza l'array in modo che tutti gli elementi minori di un elemento pivot siano a sinistra del pivot e tutti gli elementi maggiori siano a destra. Il pivot è l'elemento in posizione `low`.
>
>Ecco come funziona:
>
>1. **Input**: L'array `A` da riorganizzare, e due indici `low` e `high` che definiscono la porzione dell'array su cui operare. 
>2. **Impostazione del pivot**: Il pivot viene impostato come l'elemento in posizione `low`. 
>3. **Scansione dell'array**: La funzione scorre l'array dall'indice `low + 1` a `high`. Per ogni elemento, se è minore del pivot, lo scambia con l'elemento in posizione `i` e incrementa `i`. 
>4. **Posizionamento del pivot**: Alla fine della scansione, il pivot viene scambiato con l'elemento in posizione `i - 1`. Questo posiziona il pivot al suo posto definitivo nell'array ordinato. 
>5. **Output**: La funzione restituisce `i - 1`, che è l'indice del pivot nell'array.
>
>>[!warning] oss
>>La variabile `pivot_index` è un indice che tiene traccia della posizione in cui il pivot dovrebbe essere posizionato nell'array. Inizialmente, è impostato come `low + 1`, che è l'elemento successivo al pivot nell'array.
>>
>>Durante l'esecuzione del ciclo for, ogni volta che si trova un elemento che è minore del pivot, questo elemento viene scambiato con l'elemento alla posizione `pivot_index`, e poi `pivot_index` viene incrementato di 1. Questo assicura che tutti gli elementi a sinistra di `pivot_index` siano minori del pivot.
>    
>In pratica, la funzione `Partition` divide l'array in due parti: una con gli elementi minori del pivot e una con gli elementi maggiori o uguali al pivot. Questo è un passo fondamentale nell'algoritmo QuickSort, che funziona dividendo ripetutamente l'array in questo modo fino a quando ogni porzione è ordinata.

>[!danger] Costo Temporale
>La complessità di `Partition` $\Theta(n)$ in quanto il costo dipende dal numero di passi effettuati dal ciclo ovvero $n$.

>[!danger] Costo Spaziale
>La funzione `Partition` ha un costo spaziale costante, ovvero O(1), perché non utilizza spazio di memoria aggiuntivo proporzionale alla dimensione dell'input.
>
>Infatti modifica "in loco" la lista originale ovvero esegue le modifiche direttamente sulla struttura dati di input, senza creare nuove copie o utilizzare spazio di memoria aggiuntivo significativo.

---
### Costo Temporale

**Caso Peggiore:** 
- $O(n^{2})$
- It occurs when the pivot element picked is either the greatest or the smallest element.    

>[!warning] oss
>This condition leads to the case in which the pivot element lies in an extreme end of the sorted array. One sub-array is always empty and another sub-array contains `n - 1` elements. Thus, quick-sort is called only on this sub-array.  

**Caso Migliore:** 
- $\Omega(n\cdot \log n)$
- It occurs when the pivot element is always the middle element or near to the middle element.

**Caso Medio:** 
- $\Theta(n\cdot \log n)$ 
- It occurs when the above conditions do not occur.

![[QuikSortCost.pdf]]

---