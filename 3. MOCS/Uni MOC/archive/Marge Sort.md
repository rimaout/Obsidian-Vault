---
created: 2024-04-25
type: Uni Note
class:
  - "[[Algoritmi 1 (class)]]"
academic year: 2023/2024
related:
  - "[[Algoritmi di Ordinamento]]"
completed: true
updated: 2026-01-31T13:32
---
---

>[!abstract] Index
>1. [[#Introduzione]]
>2. [[#Funzione Merge Sort]]
>3. [[#Funzione Fondi]]

>[!abstract] Related
>- [[Algoritmi di Ordinamento]]
>- [[Algoritmi 1 (class)]]

---
## Introduzione

L’algoritmo **merge sort** (ordinamento per fusione) è un algoritmo ricorsivo che adotta una tecnica algoritmica detta [[Divide et Impera]]. 

Questo algoritmo utilizza due funzioni [[#Funzione Merge Sort|Merge Sort]] e una funzione [[#Funzione Fondi|Fondi]].

---
## Funzione Merge Sort

>[!info] Funzionamento Generale
>L’approccio dell’algoritmo Merge Sort è il seguente:
>- **Divide:** la sequenza di n elementi viene divisa in due sotto sequenze di elementi ciascuna.
>- **Impera:** le due sotto sotto sequenze di $\frac{n}{2}$ elementi vengono ordinate ricorsivamente.
>- **Passo base:** la ricorsione termina quando la sotto sotto sequenza è costituita di un solo elemento, per cui è già ordinata.
>- **Combina:** le due sotto sequenze (ormai ordinate) di $\frac{n}{2}$ elementi, vengono "fuse" in una sequenza ordinata di $n$ elementi.
>
>![[Pasted image 20240425153310.png|500]]

>[!warning] Input & Output
>Gli input della funzione `MergeSort` sono:
>- `A`: Lista che deve essere ordinata.
>- `low`: L'indice di inizio della porzione della lista che deve essere ordinata. Ad esempio, se `low = 0` verrà ordinata la lista dall'inizio.
>- `high`: L'indice di fine della porzione della lista che deve essere ordinata. Ad esempio, se `high = len(A) - 1`verrà ordinata la lista fino alla fine.
>
>L'output della funzione `MergeSort` non è un valore di ritorno, ma piuttosto un effetto collaterale: modifica la lista `A` in loco, ordinando gli elementi tra gli indici `low` e `high` inclusi. Dopo l'esecuzione della funzione, la porzione di `A` da `low` a `high` sarà ordinata in ordine crescente.
df
>[!info] Codice
>```python
def MergeSort(A, low, high):       # T(n), tempo totale
>    if low < high:                  # θ(1)
>        mid = (low + high)//2       # θ(1)
>        MergeSort(A, low, mid)      # T(n/2), tempo per ordinare la prima metà
>        MergeSort(A, mid + 1, high) # T(n/2), tempo per ordinare la seconda metà
>        fondi(A, low, mid, high)    # S(n), tempo per fondere le due metà
>```
>

>[!danger] Costo Computazionale
>
>$$
>T(n) = \begin{cases}
>2\cdot T\left( \frac{n}{2} \right) + \Theta(S(n)) & \text{se }n>1 \\
>\Theta(1) & \text{se } n\leq1
>\end{cases}
>$$
>
>dove $S(n)$ è il costo della [[#Fondi|funzione fondi]] che ha costo computazionale $\Theta(n)$
>**Quindi:**
>
>$$
>T(n) = \begin{cases}
>2\cdot T\left( \frac{n}{2} \right) + \Theta(n) & \text{se }n>1 \\
>\Theta(1) & \text{se } n\leq1 \\
>\end{cases}
>\implies T(n) = \Theta(n \log n)
>$$

---
## Funzione Fondi

>[!info] Funzionamento generale
> La funzione sfrutta il fatto che le due sotto sequenze sono ordinate;
>- l minimo della sequenza complessiva non può che essere il più piccolo fra i minimi delle due sottosequenze (se essi sono uguali, scegliere l’uno o l’altro non fa differenza);
>- dopo aver eliminato da una delle due sotto sequenze tale minimo, la proprietà rimane: il prossimo minimo non può che essere il più piccolo fra i minimi delle due parti rimanenti delle due sotto sequenze, ecc.

>[!warning] Input &  Output
>Gli input della funzione `fondi` sono:
>- `A`: Questa è la lista che deve essere ordinata. La lista `A` dovrebbe essere già ordinata in due parti: da `low` a `mid` e da `mid+1` a `high`.
   > 
>- `low`: Questo è l'indice di inizio della prima parte ordinata della lista.
>- `mid`: Questo è l'indice di fine della prima parte ordinata della lista e l'indice di inizio della seconda parte ordinata è `mid+1`. 
>- `high`: Questo è l'indice di fine della seconda parte ordinata della lista.
> 
>La funzione `fondi` fonde queste due parti ordinate in una singola parte ordinata. Dopo l'esecuzione della funzione, la lista `A` sarà ordinata dall'indice `low` all'indice `high`.

>[!info] Codice
>
>```python
>def fondi(A, low, mid, high):
>    # Puntatori per attraversare le due parti ordinate della lista + lista ordinata
>    a, b = low, mid+1
>    B = []
>
>    # Ciclo confronta gli elementi nelle posizioni correnti di a e b
>    while a <= mid and b <= high:
>        if A[a] <= A[b]:
>            B.append(A[a]) # Aggiunge l'elemento più piccolo in B
>            a += 1
>        else: 
>            B.append(A[b]) # Aggiunge l'elemento più piccolo in B
>            b += 1
>
>    #  Aggiunge eventuali elementi rimanenti da entrambe le parti in B
>    while a <= mid: 
>        B.append(A[a]) # Aggiunge gli elementi rimanenti dalla prima metà
>        a += 1
>    while b <= high:
>        B.append(A[b]) # Aggiunge gli elementi rimanenti dalla seconda metà
>        b += 1
>        
>    # Infine, copia gli elementi ordinati da B alle posizioni corrispondenti in A
>    for x in range(len(B)):
>        A[low+x] = B[x]
>```

>[!danger] Costo Computazionale
>**Costi singole parti:**
>- **Inizializzazione delle variabili:** ==$\Theta(1)$==
>- **Primo ciclo:** Ogni iterazione ha costo $\Theta(1)$ e il numero possibili di iterazione varia da $\frac{n}{2}$ a $n$. Quindi il costo è al massimo ==$\Theta(n)$== 
>- **Secondo e terzo ciclo:** I due cicli (mai eseguiti entrambi), che inseriscono eventuali elementi rimanenti in `B`, vengono eseguiti al massimo `n` volte in totale. Quindi, il costo è ==$O(n)$==
>- **L'ultimo ciclo for:** Copia gli elementi ordinati da `B` a `A`, viene eseguito `n` volte. Quindi, il costo è ==$\Theta(n)$==
>
>**Costo Complessivo:**
>
>$$
>S(n)= \Theta(1) + \Theta(n) + O(n) + \Theta(n) = \Theta(n)
>$$

---
