---
type: Uni Note
class:
  - "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related: "[[Scheduling]]"
completed: true
created: 2024-10-28T16:51
updated: 2025-02-07T22:49
---

>[!abstract] Related
>- [[Scheduling]]
>- [[Sistemi Operativi 1 (class)]]

---
## Introduzione

Ci sono diversi tipi di algoritmi che possono essere utilizzati per scegliere quale processo mandare in esecuzione, questo algoritmi variano nelle loro prestazioni e in base su quali parametri utilizzano per effettuare le scelte.

>[!note]- Schema Riassuntivo
>![[Pasted image 20241028155127.png|500]]
>
>- Le colonne indicano il tipo di algoritmo 
>- Le prime 2 righe indicano i parametri utilizzati per la scelta
>- Le restanti righe ci mostrano le caratteristiche e prestazione degli algoritmi

In particolare tutti gli algoritmi, per effettuare effettuare delle scelte utilizzano:
- [[#^79b343|Selection Function]]
- [[#^fa00bc|Decision Mode]] ^363dc9

>[!note] Selection Function
>È una formula matematica utilizzata per decidere quale processo mandare in esecuzione, si basa sulle caratteristiche dell’esecuzione come:
>- `w`: Tempo trascorso in attesa
>- `e`: Tempo trascorso in esecuzione
>- `s`: Tempo totale richiesto
>
>>**oss:** un processo appena creato avrà il tempo di esecuzione a 0  (`e = 0`) mentre il tempo totale richiesto (`s`) può essere calcolato attraverso una stima o viene fornita una _deadline_.

^79b343

>[!note] Decision Mode
>
>Specifica quando viene invocata la funzione di selezione, ci sono due modalità:
>
>
>**Non-Preemptive:** Funzione di selezione viene invocata se un processo arriva a terminazione (fine dell'esecuzione) o ad una richiesta bloccante (interrupt)
>
>**Preemptive:** Il sistema operativo può interrompere un processo in esecuzione e mandarlo in stato di _ready_. Questo blocco può avvenire o per l’arrivo di nuovi processi o per un interrupt:
>- Interrupt I/O: Un processo _blocked_ diventa _ready_
>- Clock Interrupt: Avviene in modo periodico per evitare che un processo monopolizzi il sistema

^fa00bc

---
## Algoritmi

Gli algoritmi più noti per la scelta dei processi da eseguire sono:
- [[#FCFS (First Come First Served)]]
- [[#Round Robin]]
- [[#SPN (Short Process Next)]]
- [[#SRT (Shortest Remaining Time)]]
- [[#HRRN (Highest Response Ratio Next)]]
- [[#Feedback]]

Nei sistemi operativi moderni, questi algoritmi non sono solitamente utilizzati direttamente, ma costituiscono la base per quelli utilizzati nel mondo reale. Ad esempio, Linux utilizza una versione migliorata e modificata dell'algoritmo [[#Feedback]].

>[!warning] Processi utilizzati per gli esempi
>
>Per tutti gli esempi sottostanti, utilizzeremo 5 processi batch (non interattivi) con queste caratteristiche:
>
>| Processo | Tempo di arrivo | Tempo di esecuzione | 
>| --- | --- | --- |
>| A | 0 | 3 |
>| B | 2 | 6 |
>| C | 4 | 4 |
>| D | 6 | 5 |
>| E | 8 | 2 | 

---
### FCFS (First Come First Served)

Tutti i processi vengono aggiunti alla coda dei processi ready e quando un processo smette di essere eseguito si passa a quello che ha aspettato di più in coda. È [[#^363dc9|non-preemptive]] quindi si passa ad un altro solo se termina o per interrupt.

![[Pasted image 20241028171209.png|700]]

>[!danger] Problemi
>- Un processo con poco tempo di esecuzione potrebbe dover attendere molto tempo prima di andare in esecuzione, in questo esempio `E`.
>- Favorisce i processi _CPU-Bound_ infatti dopo che uno di questi prende la CPU non la libera finché non viene interrotto o termina.

---
### Round Robin

Usa la **preemption** basandosi su un clock, spesso viene anche chiamato _time slicing_ perché ogni processo ha una “fetta” di tempo prestabilita.

>[!note] Funzionamento
>Un’interruzione di clock viene generata ad intervalli periodici. Quando l’interruzione di clock arriva, il processo attualmente in esecuzione viene rimesso nella coda dei ready. Ovviamente, se il processo in esecuzione viene bloccato da un altra interruzione viene comunque spostato nella coda dei blocked. Il prossimo processo ready nella coda viene selezionato.
>
>##### Quanto di Tempo
>
>Il quanto di tempo non è altro che l'intervallo di tempo tra i clock degli interrupt, ovvero il tempe per cui è eseguito un determinato processo prima che venga rimpiazzato.
>
>La durata di un quanto deve essere poco più lunga del “tipico” tempo di interazione per un processo. Ma se lo si fa troppo lungo, potrebbe durare più del tipico processo e il round robin degenera in [[#FCFS]]
>
>>[!column|flex] 
>>
>>>[!NOTE|no-icon] Quanto Ottimale
>>>
>>>Se maggiore del tipico tempo di interazione
>>>
>>>![[Pasted image 20241028175305.png|240]]
>>
>>>[!NOTE|no-icon] Quanto NON Ottimale
>>>
>>>Se minore del tipico tempo di interazione
>>>
>>>![[Pasted image 20241028174913.png|400]]

>[!example] Esempio
>![[Pasted image 20241028174505.png|750]]
>
>Inizialmente nel sistema è presente il processo `A` quindi, dopo una clock, interviene lo scheduler ma sceglie di nuovo `A`. Successivamente, quando altri processi sono ready, notiamo che `A` "va e viene" alternando in modo equo i processi.
>
>Notiamo che il problema presente in [[#FCFS]] con il processo `E` qui non si presenta, infatti viene eseguito non molto lontano dalla sua richiesta.

>[!danger] Problemi
>Con il round-robin, i processi CPU-bound sono favoriti usano tutto il loro **quanto** di tempo. Invece, gli I/O bound ne usano solo una porzione fino alla richiesta di I/O.
>
>Questo rende il Round Robin:
>- **non equo** 
>- **unpredictable**, ovvero aumenta la variabilità della risposta
>- **inefficiente** per i processi **I/O** bound
>
>Soluzione: [[#Round Robin Virtuale]]

#### Round Robin Virtuale

Quando un processo completa l'operazione di I/O, invece d'andare nella normale coda dei Ready, va in una nuova coda che ha priorità su quella dei ready.

Quando verrà eseguito il quanto di tempo sarà uguale alla porzione del quanto che ancora gli rimaneva da completare prima dell'interruzione I/O

![[Pasted image 20241028181951.png|350]]

---
### SPN (Short Process Next)

**SPN** sta per "Short Process Next" ovvero il prossimo processo da eseguire è il più breve, per più “breve” si intende quello il cui tempo di esecuzione stimato è minore tra quelli ready.

>[!note] Caratteristiche
>- Processi più brevi hanno la priora
>- Algoritmo [[#^363dc9|Non-Preemptive]] 
>
>![[Pasted image 20241028194958.png|550]]

>[!danger] Problemi
>- La **predicibilità** dei processi lunghi è *ridotta* ovvero, è più difficile dire quando andranno in esecuzione.
>- Se il **tempo di esecuzione** stimato si rivela **inesatto**, il sistema operativo può *abortire\* il processo.
>- I **processi lunghi** potrebbero soffrire di *starvation*.

>[!warning] Stima del tempo di esecuzione
>In sistemi dove alcuni processi sono eseguiti più volte è possibile stimare il tempo di esecuzione guardando alle precedenti esecuzioni, ed esistono due tecniche
>
>>**oss:** Si indica il tempo passato con $T_{i}$ e futuro con $S_{i}$ si indica la stima, e l'indice $i$ indica il numero di volte che è stato eseguito il processo
>
>
>$$
>\begin{align*}
>1. \ \ \ S_{n+1} &= \frac{1}{n} \cdot  \sum^{n}_{i=1} T_{i} \\ 
>2. \ \ \ S_{n+1} &= \frac{1}{n}T_{n} + \frac{n-1}{n}S_{n}
>\end{align*}
>$$
>
>Questa formula non fa altro che prendere tutti i tempi di esecuzione precedenti e ne calcola la media. È 
>
>>**Importante** notare che se si utilizza la seconda formula non serve salvare tutti i tempi di esecuzione ma semplicemente l'ultimo tempo tempo ($T_{n}$) e l'ultima stima ($S_{n}$).
>
>Esiste anche una formula più avanzata che da maggiore importanza ai tempi di esecuzione delle esecuzioni più recenti (**Exponential averaging**) 
>
>$$
>S_{n+1} = \alpha \cdot  T_{n} + (1-\alpha) \cdot S_{n}\\
>$$
>
>>**oss:** $\alpha$ è un valore compreso tra $0$ e $1$ dove mettendo valori alti permette di dare più importanza alle esecuzioni più recenti.
>
>>[!column|flex] 
>>
>>>[!NOTE|no-icon] Esempio con diversi calori di alpha
>>>
>>>![[Pasted image 20241028202341.png|450]]
>>
>>>[!NOTE|no-icon] Esempio tra media normale ed esponenziale
>>>
>>>![[Pasted image 20241028202456.png|450]]

---
### SRT (Shortest Remaining Time)

Come [[#SPN (Short Process Next)|SPN]] esegue il processo più corto presente nel sistema, ma è **preemptive**, quindi non ha una **time quantum** ma si basa sul fatto che esegue un controllo per scegliere il processo più corto ad ogni arrivo di un nuovo processo appena creato, o alla fine del processo in esecuzione.

![[Pasted image 20241031172730.png|700]]

---
### HRRN (Highest Response Ratio Next)

Anche questo algoritmo necessita di conoscere il tempo di risposta di un processo, in questo caso **non può avvenire starvation** e non è [[#^363dc9|preemptive]].

Questo algoritmo esegue il processo che ha come valore più alto:
$$
\frac{w+ s}{s} = \frac{\text{Tempo trascorso in attesa + Tempo totale richiesto​}}{\text{Tempo totale richiesto}}
$$

Quindi non prende in considerazione soltanto il tempo di esecuzione del processo ma anche da quanto tempo sta aspettato.

![[Pasted image 20241106192207.png|750]]