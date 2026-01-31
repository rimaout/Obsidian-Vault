---
type: Uni Note
class:
  - "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related: "[[Scheduling]]"
completed: true
created: 2024-10-27T15:31
updated: 2026-01-31T13:32
---
[!abstract] Related
>- [[Scheduling]]
>- [[Sistemi Operativi 1 (class)]]

---
## Introduzione

Un sistema operativo deve allocare risorse tra diversi processi che ne fanno richiesta contemporaneamente
Tra le diverse possibili risorse, c’è il **tempo di esecuzione** fornito da un processore.

Il meccanismo che si occupa della gestione di questa risorsa si chiama scheduling.

>[!note] Scopo
>Assegnare ad ogni processore i processi da eseguire, man mano che i processi stessi vengono creati e distrutti.
>
>Tale obiettivo va raggiunto ottimizzando vari aspetti:
>- tempo di risposta
>- throughput
>- efficienza del processore (meno tempo il processore è inattivo meglio è)

>[!note] Obbiettivo
>Distribuire il tempo di esecuzione in modo equo tra i vari processi senza favoritismi, ma allo stesso tempo deve tener conto delle priorità dei processi quando necessario.
>
>**Obbiettivi:** 
>- Evitare la starvation (letteralmente, morte per fame) dei processi
>- Usare il processore in modo efficiente 
>- Avere un overhead basso
>  
>Overhead basso, significa che il processo stesso dello Scheduling deve essere efficiente e non occupare più tepo del dovuto il processore.

---
## Tipi di Scheduling

Esistono diversi tipi di Scheduler che variano nel quanto spesso vengono eseguiti:
- [[#Long-Term Scheduling]]: decide l’aggiunta ai processi da essere eseguiti
- [[#Medium-Term Scheduling]]: decide l’aggiunta ai processi che sono in memoria principale
- [[#Short-Term Scheduling]]: decide quale processo, tra quelli pronti, va eseguito da un processore
- **I/O scheduling:** decide a quale processo, tra quelli con una richiesta pendente per l’I/O, va assegnato il corrispondente dispositivo di I/O

>[!note] Stati dei processi e scheduling
>Prendendo come esempio il [[Processi#^458367897|modello a 7 stati (2 stati sospesi)]]:
>
>![[Pasted image 20241006110217.png|400]]
>
>Queste sono le transizioni decisi dai vari scheduler:
>
>![[Pasted image 20241027160050.png|400]]
>
>>**oss:** il medium-term scheduler, in realtà, è responsabile anche dell’altro verso delle due frecce mostrate (  `Blocked/Suspended` <- `Blocked`)
>
>![[Pasted image 20241027160300.png|500]]

---
## Long-Term Scheduling

Decide quali programmi sono ammessi nel sistema per essere eseguiti:
- spesso è FIFO (first in first out) ovvero il primo che entra nella coda è il primo ad essere eseguito.
- altrettanto spesso, è un FIFO “corretto”, ovvero che tiene conto di criteri come priorità, requisiti per l’I/O o tempo di esecuzione atteso.

>**oss:** più processi ci sono, più è piccola la percentuale di tempo per cui ogni processo viene eseguito.


>[!note] Strategie
>
>**Processi interattivi vs Processi Batch:**
>- I lavori di batch (ovvero i processi non iperattivi) vengono semplicemente inseriti nella coda FIFO e verranno eseguiti man mano che arriverà il loro turno.
>- I lavori interattivi vengono subito eseguiti fino a saturazione del sistema (messi alla fine della cosa, quindi saltano tutti lavori batch)
>  
>**I/O Bound vs CPU Bound:**
>- se si sa quali processi sono I/O bound e quali CPU-bound, si può mantenere un giusto mix tra i 2 tipi.
>- se si sa quali processi fanno richieste a quali dispositivi di I/O è possibile bilanciare tali richieste, per evitare che due processi in esecuzione richiedano accesso alla stessa risorsa allo stesso momento.

---
## Medium-Term Scheduling

Il **Medium-Term Scheduling** si occupa della gestione del *memory swap* ovvero il passaggio delle informazioni associate ad un processo dalla memoria principale (ram) alla memoria secondarie (disco).

Importante per il controllo del grado di multiprogrammazione b

---
## Short-Term Scheduling (dispatcher)

Viene chiamato anche **dispatcher**, è lo scheduler eseguito più frequentemente e viene invocato in seguito a seguiti di alcuni eventi:
- Interruzioni di clock (fanno parte degli interrupt)
- Interruzioni I/O
- Chiamate di sistema
- Segnali
- alto ...

>[!note] Scopo
>Il suo scopo è quello di ottimizzare l’intero sistema decidendo che programma mandare in esecuzione, ma per valutare una **politica di scheduling** vanno definiti dei criteri:

>[!note] Criteri
>
>>Distinzione tra Criteri Utente e Criteri Sistema.
>- **Criteri Utente:**  tempo di risposta ovvero, il tempo che passa tra la richiesta di una computazione e la visualizzazione dell’output
>- **Criteri si Sistema:** uso efficiente ed effettivo del processore
>  
>>Un’altra distinzione che va fatta è tra Criteri Prestazionali e Criteri non Prestazionali
>
>Criteri **Utente Prestazionali:**
>- [[#Turn-Around Time]] (tempo di ritorno)
>- [[#Response Time]]
>- [[#Deadline e Predicibilità|Deadline]]
>
>Criteri **Utente Non Prestazionali:**
>- [[#Deadline e Predicibilità|Predictability]]
>
>Criteri di **Sistema Prestazionali:**
>- [[#Throughput]] (volume di lavoro nel tempo)
>- [[#Processor Utilization]]
>
>Criteri di **Sistema Non Prestazionali:**
>- [[#Fairness e priorità|Fairness]] (equità)
>- [[#Fairness e priorità|Enforcing Priorities]] (gestione priorità)
>- [[#Bilanciamento Risorse|Balancing Resources]] (bilanciamento uso risorse)
>
 >>[!warning] Osservazione
 >>I criteri *prestazionali* sono correlati alle prestazioni, quindi sono *quantitativi* e facili da misurare
 >>
 >>I criteri *non prestazionali* sono *qualitativi* e quindi difficili da misurare

---
## Criteri Dello Short Term Scheduling 

Ora approfondiamo tutti i criteri visti precedentemente per lo short tern scheduling

#### Turn-Around Time

È il tempo che passa tra la creazione di un processo creato dall’utente e il suo completamento, questo comprende anche i vari tempi di attesa di I/O. È un criterio spesso utilizzato per i processi non interattivi.

#### Response Time

Questo è più utilizzato per i processi interattivi, è il tempo tra l’invio del programma e il suo completamento.

Lo scheduler ha due obiettivi in questo caso:
- Minimizzare il tempo di risposta
- Massimizzare il numero di utenti con un buon tempo di risposta
#### Deadline e Predicibilità

Ci sono dei sistemi operativi che ci permettono di dare una deadline ai processi, ovvero possiamo inserire un tempo massimo di esecuzione. Lo scheduler cerca di rispettare questo limite imposto dall’utente e il suo obiettivo è quindi quello di massimizzare il numero di scadenze rispettate.

Per quanto riguarda la predicibilità, l’utente non vuole che ci sia troppa variabilità nei tempi di risposta, ad esempio un programma ci mette 5 secondi e un altro 1, oppure se lanciamo più volte lo stesso programma ci aspettiamo sempre il solito tempo di esecuzione. Ovviamente con alcune eccezioni particolari come ad esempio RAM satura.

#### Throughput

È il numero di processi che il sistema riesce a completare in un certo tempo, lo scheduler ovviamente vuole massimizzare questo valore. Ci dà una misura su quanto lavoro viene effettuato e ovviamente dipende anche dai tempi di esecuzioni dei processi

#### Processor Utilization

L'utilizzo del processore è la percentuale di tempo in cui il processore viene utilizzato, lo scheduler deve fare in modo che il processore sia in idle il minor tempo possibile, quindi deve fare in modo che ci siano processi _ready_.

Questo è molto utile su sistemi condivisi tra più utenti.

#### Bilanciamento Risorse

Lo scheduler deve fare in modo che le risorse vengano usate il più possibile, quindi il sistema favorisce i processi che usano le risorse attualmente sotto utilizzate (evitando che processi che utilizzano le stesse risorse siano tutti in esecuzione allo stesso momento).

#### Fairness e priorità

Se non ci sono specifiche sulla priorità allora tutti i processi devono essere trattati allo stesso modo, se c’è vanno favoriti quelli con priorità più alta, ogni priorità avrà una coda.

Non deve verificarsi _starvation_ ovvero come detto prima, processi che aspettano la loro esecuzione senza mai andarci.
  
>[!danger] Priorità e Starvation
>Da notare che la priorità può causare la starvation, infatti un processo a bassa priorità potrebbe soffrire di starvation a causa di un processo a priorità più alta, come soluzione possiamo fare in modo che man mano che “l’età” del processo aumenta, aumenta anche la sua priorità. Oppure anche in base a quante volte è andato in esecuzione.

