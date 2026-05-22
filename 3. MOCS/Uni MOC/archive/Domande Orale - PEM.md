---
type: Uni Note
class:
  - "[[Programmazione Sistemi Multicore (class)]]"
academic year: 2024/2025
related:
completed: false
created: 2026-04-13T20:30
updated: 2026-05-22T17:03
---
>[!danger] Good to know
>
>>[!note]- MPI nonovertaking messages
>>MPI requires that messages be *nonovertaking*. This means that if process q sends two messages to processr, then the first message sent by q must be available tor before the second message.
>>
>>However, there is no restriction on the arrival of messages sent from different processes

## Generali

>[!note]- 1.1 Cos'è il False Scaring? 🟠
>
>Il _false sharing_ è un "effetto collaterale" dei sistemi di coerenza della cache che porta ad un degradamento delle performance. Si verifica quando due o più thread, in esecuzione parallela su core diversi, modificano variabili logicamente distinte che però risiedono fisicamente all'interno della stessa linea di cache (_cache line_).
>
>Per comprendere il problema, occorre ricordare che i dati non vengono trasferiti dalla memoria principale alla cache del processore come singole variabili, ma a blocchi di dimensione fissa chiamati, appunto, cache line. Ad esempio, in un'architettura con cache line da 64 Byte, un singolo blocco può contenere fino a 16 interi da 4 Byte adiacenti in memoria.
>
>Il collo di bottiglia prestazionale sorge a causa del meccanismo di coerenza della cache hardware: quando un thread modifica la propria variabile, l'intero blocco di cache viene contrassegnato come "invalido" per tutti gli altri core. Di conseguenza, gli altri thread saranno costretti a ricaricare l'intera linea dalla memoria principale (o da una cache condivisa di livello superiore), anche se stavano lavorando su variabili completamente diverse e non modificate.
>
>Come risolvere il False Sharing?
>
>Per mitigare o eliminare questo problema si utilizzano principalmente tre strategie:
>
>- **Data Padding (Riempimento):** Consiste nell'inserire dello spazio vuoto (byte di _padding_) tra le variabili utilizzate dai diversi thread. In questo modo si "allontanano" i dati in memoria, costringendoli a risiedere su cache line separate. 
>- **Allineamento della memoria (Alignment):** Sfruttare direttive del compilatore (come `alignas` in C++ o `@Contended` in Java) per allineare l'indirizzo di inizio di una struttura dati esattamente al confine di una cache line.
>- **Localizzazione dei dati (Thread-local storage):** Progettare l'algoritmo in modo che ogni thread lavori principalmente su zone di memoria separate o su copie locali dei dati (es. registri o stack privato), accumulando i risultati in una struttura globale solo al termine dell'elaborazione.

>[!note]- 1.2 Differenze tra Array of Structs (AOS) e Struct of Arrays (SOA) 🟠
>
>Ovviamente la principale differenza è come vengono rappresentate in memoria:
>- Nell'**AoS** (Array of Struct), dichiariamo un array in cui ogni elemento è una struttura (es. con campi `x` e `y`). In memoria, i dati di ogni singola struttura sono alternati e contigui: `x y | x y | x y`.
>- Nel **SoA** (Struct of Array), abbiamo un'unica struttura contenente array separati per ogni campo. In memoria, tutti i valori dello stesso tipo sono raggruppati insieme: `x x x x | y y y y`."
>
>Questi layout hanno differenze quando si vuole ottimizzare la **cache locality**:
>- Se usiamo l'*AoS*, quando il thread porta in cache il dato `x`, la cache line si riempirà anche dei valori `y` adiacenti.
>- Con il *SoA*, invece, poiché tutte le `x` sono vicine, il caricamento in cache porta solo i valori `x` adiacenti .
>
>Quindi se un calcolo utilizza solo dei valori `x` (e non gli `y`) allora conviene utilizzare *SoA*.
>
>Nella programmazione su **GPU**: il vantaggio principale del *SoA* è che abilita i cosiddetti **coalesced accesses** (accessi coalescenti). Poiché i thread paralleli accedono a indirizzi di memoria strettamente contigui (il thread 0 accede a $x_0$, il thread 1 a $x_1$, ecc., che sono uno di fianco all'altro), l'hardware può "combinare" queste richieste in un'unica singola transazione di memoria, massimizzando la banda passante.
>
>Infine, c'è un vantaggio anche in termini di **occupazione di memoria** grezza. Le strutture in C spesso richiedono l'inserimento di byte vuoti (**padding**) per mantenere l'allineamento in memoria. Nell'AoS, questo padding potrebbe essere necessario dopo _ogni singola struttura_ dell'array, sprecando molta memoria. Nel SoA, avendo array omogenei di tipi base (come array di soli float), il problema dell'allineamento interno è quasi inesistente, richiedendo complessivamente meno spazio.
>
>In realtà i SOA sono anche meglio per la vettorizazione, in quanto per fettuare operazioni simd i valori devono essere contingui in memoria.
>
>>[!warning] Slides
>>![[Pasted image 20260506114304.png|500]]
>>![[Pasted image 20260506114254.png|500]]
>>![[Pasted image 20260506114320.png|500]]

>[!note]- 1.3 Tra AOS e SOA, chi occupa più memoria? 🟠
>
>Appunti prof: SoA might also require less space (AoS might have padding after each struct)
>
>Un ulteriore vantaggio del SoA è la riduzione dello spreco di memoria dovuto al **padding**. Nell'AoS, se abbiamo strutture con tipi di dato di dimensioni diverse, il compilatore inserisce byte vuoti di allineamento che vengono ripetuti per ogni elemento dell'array. Nel SoA, raggruppando dati omogenei in array separati, il problema dell'allineamento interno viene eliminato, compattando enormemente i dati in memoria.
>```c
>struct Particella { 
>	bool attiva; // Occupa 1 byte 
>	// <--- IL COMPILATORE INSERISCE 3 BYTE DI PADDING (SPAZIO VUOTO) QUI 
>	float peso; // Occupa 4 byte 
>}; 
>
>struct Particella AoS[1000];
>```
>
>```c
>struct ParticelleSoA { 
>	bool attiva[1000]; // 1.000 byte contigui. Nessun padding interno! 
>	float peso[1000]; // 4.000 byte contigui. Nessun padding interno! 
>}; 
>
>struct ParticelleSoA SoA
>```

>[!note]- 1.4 Data una percentuale di codice sequenziale, qual'è lo speed up massimo ottenibile? 🟠
>
>Secondo la Legge di Amdahl, lo speed-up $S(p)$ di un programma è strettamente limitato dalla sua frazione sequenziale. Se indichiamo con $\alpha$ la percentuale di codice parallelizzabile e con $1 - \alpha$ la percentuale di codice sequenziale, lo speed-up massimo teorico si ottiene calcolando il limite per il numero di processori $p$ che tende a infinito:
>
>$$
>\frac{1}{1-\alpha}
>$$
>
>Per esempio, se abbiamo un'applicazione in cui il **60%** del codice è parallelizzabile, significa che $\alpha = 0.6$. La frazione sequenziale sarà $1 - 0.6 = 0.4$. Lo speed-up massimo che potremo mai ottenere sarà $\frac{1}{0.4} = 2.5$.
>
>---
>
>Come si ottiene questa formula:
>
>Sia $T_s$ il tempo di esecuzione sequenziale, Sia $T_{p}(p)$ il tempo di esecuzione del programma parallelizzato con `p` processori.
>
>$$T_{p}(p) = (1 − \alpha)T_{s} + \alpha\frac{ T_{s}}{p}$$
>
>Dove $\alpha ∈ [0, 1]$ rappresenta la frazione parallelizzabile, e $1 − α$ la frazione seriale.
>
>
>Lo speed up sarà quindi:
>$$S(p) = \frac{T_{s}}{T_{p}(p)} = \frac{T_{s}}{(1 − α)T_{s}\ +\  \alpha \frac{T_{s}}{p}}$$
>
>Il valore dello speed up è limitato superiormente, infatti all’aumentare dei processi:
>
>$$\lim_{ p\to \infty } S(p) = \lim_{ p \to \infty } \frac{T_{s}}{(1 − α)T_{s}\ +\  \alpha \frac{T_{s}}{p}} = \frac{T_{s}}{(1 − α)T_{s}} = \frac{1}{(1 − α)}$$

>[!note]- 1.5 Cosa sono l'Amdahl e la Gustafson laws? 🟠
>
>Sono due leggi che permettono di studiare a livello teorico lo scaling ideale di un programma parallelizzato.
>
>La legge di Amdahl studia lo strong scaling, in cui abbiamo un problema di dimensione fissa `n`, con $T_{s}$ definiamo tempo del esecuzione sequenziale, e con $T_{p}(p)$ il tempo di esecuzione parallela con `p` processori.
>
>Che lo speedup massimo è descritto dalla seguente formula: $S(p) = \frac{T_{s}}{\lim_{ p \to \infty } T_{p(p)}} = \frac{1}{1 - \alpha}$
>
>Dove $\alpha$ è la sezione del problema che è paralellizabile, e $1-\alpha$ è la sezione di programma non parallelizzabile.
>
>La Gustafson law invece tiene conto dello week scaling, ovvero che all'aumentare del numero di processori, aumenta in modo proporzionale anche la dimensione del programma.
>
>$$
>S(p) = \frac{(1-\alpha) + \alpha p}{(1-\alpha) + \alpha} =  \frac{(1-\alpha) + \alpha p}{1} = (1-\alpha) + \alpha p
>$$
>
>---
>
>**Limitazioni dell'Amdahl Law e Gustafson Law**: danno per scontato che la dimensione della parte seriale rimanga costante all'aumentare del numero di processori, ma questo nel mondo reale raramente è vero.

>[!note]- 1.6 Cos'è il Roofline Model? 🔴

>[!note]- 1.7 Cos'è il tiling? 🟠
>
>Il **tiling** è una tecnica di ottimizzazione per gli accessi in memoria per la programmazione GPU.
>
>Consiste nel suddividere grandi strutture dati (tipicamente matrici) in blocchi più piccoli e gestibili chiamati **"tiles"**.
>
>L'idea centrale è caricare questi tasselli nella **shared memory** della GPU invece di continuare a leggerli dalla memoria globale, il titiling è necessario in quanto la shared memory solitamente non è abbastanza grande per contenere i dati per intero..
>
>In un'implementazione con tiling, i thread di uno stesso blocco collaborano: ogni thread carica una piccola porzione della "tile" dalla memoria globale alla shared memory. Poi vengono effettuati i calcoli se qui dati. Una volta finito si caricano in shared la nuova tile.
>
>Questo permette di **ridurre il traffico verso la memoria globale**. Poiché la memoria globale è lenta (alta latenza) mentre la shared memory è molto veloce (on-chip, simile alla cache L1), riutilizzare i dati caricati nella shared memory aumenta drasticamente l'efficienza.

>[!note]- 1.8 Cos'è la Pinned Memory? 🔴

>[!note]- 1.9 Com'è gestito un read-write lock? 🟠
>
>Un **read-write lock** (RW lock) è un meccanismo di sincronizzazione, simile a una mutex, progettato per gestire l'accesso a strutture dati condivise in modo più efficiente quando le operazioni di sola lettura sono molto frequenti rispetto a quelle di modifica.
>
>Ecco come viene gestito e quali sono le sue regole di funzionamento:
>
>Logica di Accesso
>
>La caratteristica principale di un read-write lock è la distinzione tra l'accesso in lettura e quello in scrittura:
>
>- **Lettura multipla:** Più thread possono ottenere contemporaneamente il lock in lettura e accedere alla risorsa, a patto che nessun thread detenga o abbia richiesto il lock in scrittura.
>- **Scrittura esclusiva:** Solo un thread alla volta può ottenere il lock in scrittura. Mentre un thread scrive, nessun altro thread può accedere alla risorsa, né in lettura né in scrittura.
>
>Interazioni tra i Lock
>
>La gestione delle attese segue regole precise basate sullo stato attuale della risorsa:
>- **Se la risorsa è libera:** Un thread può ottenere immediatamente sia un lock in lettura che uno in scrittura.
>- **Se c'è un lock in lettura attivo:**
>    - Altri thread che richiedono un **lock in lettura** lo ottengono immediatamente.
>    - Thread che richiedono un **lock in scrittura** devono attendere che tutti i lettori correnti rilascino la risorsa.
>- **Se c'è un lock in scrittura attivo:**
>    - Qualsiasi altra richiesta (sia di lettura che di scrittura) viene messa in attesa fino al rilascio del lock.
## MPI

>[!note]- 2.1 `MPI_Status` fields: in which cases do we need to get the missing tag or rank using `MPI_Status`? 🔴

>[!note]- 2.2 MPI Errors 🔴
>
>

>[!note]- 2.3 How do we get the number of elements we have received in a communication? Why could we receive fewer elements than `buf_size`? 🔴

>[!note]- 2.4 What are the different levels of threading in MPI? (funneled, serialized, ...). What's the difference? 🔴
>

>[!note]- 2.5 What are derived datatypes in MPI? 🔴

>[!note]- 2.6 Discuss the different types of `MPI_Send` 🔴

>[!note] 2.7 How would you sum up two matrices using MPI? 🔴

>[!note]- 2.8 When could you have a deadlock in MPI? 🔴

>[!note]- 2.9 Which problem does `MPI_SendRecv` solve? 🔴

>[!note]- 2.10 How does `MPI_IN_PLACE` work? 🔴

>[!note]- 2.11 How does communication between GPUs work in MPI? 🔴

## OpenMP

>[!note]- 3.1 How do nested loops work and how do we manage them in OpenMP? 🔴

>[!note]- 3.2 How does variable scoping work in OpenMP? 🔴

>[!note] 2.4 How does scheduling work in OpenMP? 🔴

>[!note] 2.5 Parallelize a loop which performs the element-wise product of two arrays with OpenMP 🔴

>[!note] 2.6 Parallelize the following `for` cycles: 🔴
>```c
>for(int i = 2; i < N; i++) {
>	A[i] = A[i - 2] + A[i] * 0.5; 
>}
>
>//-------------------------------
>
>for(int i = 1; i < N; i++) {
>	for(int j = 1; j < M; j++) {
>		d[i][j] = d[i][j-1] + d[i-1][j-1] + d[i-1][j];
>	}
>}
>```
>
>>[!example]- Response
>>kjfhskd

## CUDA

>[!note]- 3.1 What are memory banks? When do we have bank conflicts and bank broadcast? 🔴
>

>[!note]- 3.2 When does it make sense to disable L1 cache in CUDA? 🔴

>[!note]- 3.3 Why is there no false sharing on GPU? 🔴

>[!note]- 3.4 Scrivi un CUDA kernel che effettua la somma di due array ✅
>
>```c
>__gobal__ void arrSum(int* d_A, int* d_B, int* d_C, int n) {
>	int gid = (blockDim.x * blockIdx.x) + threadIdx.x;
>	
>	if (gid < n) { 
>		d_C[gid] = d_A[gid] + d_B[gid]
>	}
>}
>```

>[!note]- 3.5 Scrivi un CUDA kernel che calcola l'(element-wise) product between two arrays. ✅
>
>```c
>__gobal__ void arrMult(int* d_A, int* d_B, int* d_C, int n) {
>	int gid = (blockDim.x * blockIdx.x) + threadIdx.x;
>	
>	if (gid < n) { 
>		d_C[gid] = d_A[gid] * d_B[gid]
>	}
>}
>```

>[!note] 3.6 Write a CUDA kernel that computes the product between two matrices

```
int temp;
out[n][m];

for i in 0..n:
	for j in 0..m:
		temp += m1[i][j] * m2[j][i]
	
		out[i][j] = temp		
	
```

 >[!note] 3.7 What does it mean that memory accesses are coalesced? 🔴
>

>[!note] 3.8 What is the more convenient on GPU, Array of Structs or Struct of Arrays? 🔴
>
>

>[!note]- 3.9 How does `cudaMemcpy()` work between CPU and GPU? 🔴
