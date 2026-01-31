---
type: Uni Note
class: "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related:
completed: false
created: 2024-11-23T13:04
updated: 2026-01-31T13:32
---
>[!abstract] Related
>- 

---
## Introduzione

La memoria virtuale consente di eseguire un processo anche se non tutte le sue pagine sono in memoria principale. L'unica cosa necessaria è che la *prossima istruzione* e i dati di cui ha bisogno siano in *memoria principale*.

Il sistema operativo carica in memoria principale solo alcune parti del programma (resident set[^1]) e genera un interrupt (*page fault*[^2]) quando il processo richiede un indirizzo che non si trova in memoria principale. 

Quando avviene un *page fault* Il sistema operativo mette il processo in modalità "blocked" e richiede la lettura del pezzo di processo mancante da disco. Una volta completata la lettura, il processo torna in modalità "ready" e può essere eseguito nuovamente. 

>[!note] Benefici
>- Riduce lo spazio della memoria virtuale utilizzato da ogni processo
>- Aumenta il numero di processi che possono essere contemporaneamente in memoria principale - anche se non per intero - e di utilizzare al meglio il processore senza renderlo idle.
>
>Grazie a questo possiamo avere molti più processi in RAM, quindi il processore passa poco tempo in idle e inoltre un processo potrebbe richiedere più dell’intera memoria principale.

---
### Terminologia

Con **memoria virtuale** intendiamo uno schema di allocazione in cui la memoria secondaria può essere usata come se fosse principale.

- Gli indirizzi dei programmi sono logici mentre quelli usati dal sistema sono fisici
- C’è bisogno di una traduzione dai logici a fisici
- La dimensione di questa memoria è limitata oltre che dalla sua grandezza anche dallo schema di indirizzamento
- La dimensione della RAM invece non influisce sulla dimensione della virtuale.

>[!note] Definizioni
>- ***Indirizzo Virtuale:*** Sono come gli indirizzi logici, fanno in modo che si possa accedere a locazioni della memoria virtuale come se fossero locazioni della principale.
>- ***Spazio indirizzi virtuali:*** La quantità di memoria virtuale assegnata ad un processo
>- ***Spazio degli indirizzi:*** Quantità di memoria assegnata ad un processo
>- ***Indirizzo Reale:*** Indirizzo di una locazione di memoria principale, sarebbe l’indirizzo fisico.
>

>[!danger] TLDR
>- ***Memoria Reale:*** Indichiamo la memoria principale (RAM)
>- ***Memoria Virtuale:*** Quella su disco, ci permette di avere multiprogrammazione elevata liberando il programmatore dai vincoli della principale

---
### Effetti Collaterali

>[!note] Thrashing
>Il Sistema Operativo impiega troppo tempo a swappare pezzi di processi da RAM a disco o viceversa, accade ad esempio quando ci sono troppi page fault.
>
>>***Soluzione:***
>>Per evitarlo il S.O. cerca di indovinare quali pezzi di processo saranno richiesti nella prossima istruzione, questo tentativo si basa sulla storia recente.
>>
>>I riferimenti che un processo fa tendono ad essere vicini, quindi solo pochi pezzi di processo saranno necessari di volta in volta, è possibile quindi prevedere quali pezzi di processo saranno necessari in futuro. Funziona simile alla cache quindi.

>[!note] Supporto Hardware
>La memoria virtuale per funzionare ha bisogno di supporto hardware, se cosi non fosse richiederebbe troppo overhead. 
>
>In particolare la *traduzione degli indirizzi* e lo *spostamento delle pagine* e/o segmenti dalla memoria principale alla secondaria è hardware.

---
## Paginazione

Precedentemente abbiamo visto la [[Paginazione e Segmentazione (semplice)#Paginazione Semplice|paginazione semplice]] ora vediamo come viene implementa utilizzando anche la memoria virtuale.

>[!note] Tabella delle Pagine
>Ogni processo ha una sua tabella delle pagine, ogni entry di questa tabella contiene:
>- Un bit di presenza che indica se quella pagina è in RAM o se bisogna prenderla su disco
>- Un bit che indica se la pagina è stata usata in lettura o anche scrittura
>- Altri bit di controllo
>- Il numero di frame in memoria principale
>  
>![[3. MOCS/Uni MOC/archive/attachments/Pasted image 20241123143824.png|400]]

### Traduzione degli indirizzi

Un *indirizzo virtuale* è composto da due parti il *numero di pagina* e l'***offset***. L'obbiettivo è tradurre un indirizzo virtuale in un indirizzo fisico, per fare ciò si inizia da un indirizzo virtuale:

>[!note] Traduzione degli indirizzi (base)
>
>Prendiamo il numero di pagina e lo moltiplichiamo per la grandezza di ogni pagina e poi sommiamo il risultato con l'indirizzo puntato dal *Page Table Ptr*[^3], cosi facendo otteniamo il ***numero del frame*** all interno della tabella delle pagine
>
>Per "creare" l'indirizzo fisico dobbiamo unire il ***numero del frame*** di attivazione all'***offset*** presente nell'indirizzo virtuale.
>
>![[3. MOCS/Uni MOC/archive/attachments/Pasted image 20241123154946.png|700]]
>
>>***Svantaggio:*** Questa struttura porta però a molto overhead, le tabelle potrebbero contenere molti elementi. 
>
>>[!warning]- Esempio di overhead
>>Quando un processo è in esecuzione, è assicurato che almeno una parte della sua tabella delle pagine sia in memoria principale, vediamo qualche conto:
>>
>>Abbiamo 8Gb di spazio virtuale e 1kb per ogni pagina, quindi in totale possiamo avere $\frac{8GB}{1KB}$​ di entry per ogni tabella, questo significa che per ogni processo abbiamo 223 entries (divisione ma in binario), necessari a indicizzare tutti i frames della RAM. (8 giga è $2^{33}$ mentre 1kb è 210)
>>
>>Quanto spazio occupa una entry? Ha 1 byte per i bit di controllo + $log(\text{Grandezza della RAM in frames})$ quindi ad esempio con 4GB di RAM abbiamo indirizzi da massimo 32 bit, ne togliamo 10 per le pagine da 1kB ci rimangono 22 bit per il _Frame Number_ della entry, quindi in totale abbiamo 3 bytes per il frame number più un byte per i bit di controllo.
>>
>>Se abbiamo $2^{23}$ entries allora dobbiamo fare $4 \cdot 2^{23} = 32\text{MB}$  di overhead per ogni processo.
>>
>>Ad esempio con una RAM da 1Gb, bastano 20 processi a occupare più di metà RAM in overhead.

^bd6ece

>[!note] Traduzione con tabelle delle pagine a 2 livelli
>
>Per risolvere il problema dell’overhead della [[#^bd6ece|traduzione degli indirizzi (base)]] si utilizza un sistema a 2 (o più) tabelle delle pagine.
>
>![[3. MOCS/Uni MOC/archive/attachments/Pasted image 20241123175547.png|800]]
>
>In questo caso abbiamo una tabella che invece di puntare direttamente a zone di RAM punta ad un’altra tabella che poi punta allo spazio utente
>
>***Funzionamento della traduzione:***
>- Funzionamento identico alla versione "[[#^bd6ece|base]]" ma l’hardware deve consultare due tabelle
>- Da notare che che adesso l’indirizzo virtuale è diviso in 3 sezioni, in generale in n.livelli + 1.
>
>![[3. MOCS/Uni MOC/archive/attachments/Pasted image 20241123180333.png|900]]
>
>>[!warning]- Esempio di overhead
>>Vediamo perché conviene facendo dei conti.
>>
>>Abbiamo 8GB di spazio virtuale e quindi 33 bit di indirizzo, supponiamo di utilizzare 10 bit per l’offset quindi come prima abbiamo pagine da 1kB, i restanti 23 li dividiamo in 15+8, i 15 bit li usiamo per il primo livello e gli 8 per il secondo. Per rendere più efficiente il tutto una tabella di secondo livello deve essere grande quanto una pagina.
>>
>>Ogni processo ha quindi un overhead di $2^{23+2} = 32MB$ infatti deve contenere tutte le entries di entrambe le tabelle e in più un ulteriore overhead di $2^{15+2}=128KB$ solo per il primo livello.
>>
>>Adesso è sufficiente caricare in RAM il primo livello che è molto poco e una tabella del secondo e quindi per ogni processo $2^{15+2}$ di overhead che è circa 128KB, con una RAM da 1GB servono circa 1000 processi per occupare metà RAM.
>
>***RIVEDI 2° VIDEO DELLA GESTIONE MEMORIA:*** time-stamp: `1:03:00`

---
## TLB - Translation Lookaside Buffer

**Traduzione:** Memoria temporanea per la traduzione futura

>[!danger] Problema da risolvere
>Ogni riferimento alla memoria virtuale può generare due accessi alla memoria
>- uno per la tabella delle pagine
>- uno per prendere il dato
>  
>***Soluzione:*** si usa una cache per gli elementi della tabella delle pagine, questo contiene indirizzi di frame. Questo è il TLB.

>[!note] Funzionamento
>Dato un indirizzo virtuale il processore non va subito a fare la traduzione ma prima consulta il TLB.
>
>***TLB Hit:*** Se la pagina è presente nel TLB allora si prende il frame number e si ricava l’indirizzo reale. 
>
>***TLB Miss:*** Se la pagina NON è presente nel TLB allora prende la tabella delle pagine del processo ed effettua i normali calcoli, dopo di che si hanno due possibilità:
>- la pagina si trova in memoria ed è possibile accederla
>- la pagina NON si trova in memoria quindi si gestisce il page fault
>
>>***oss:*** Dopo un page miss si aggiorna il TLB includendo la pagina appena acceduta, usando algoritmi di rimpiazzo se necessario proprio come una cache.
>
>![[3. MOCS/Uni MOC/archive/attachments/Screenshot 2024-11-24 at 10.20.49.jpg|1300]]

Il TLB è totalmente hardware, ma in alcune situazioni il sistema operativo prende il controllo.

L'OS ha il compito di effettuare il reset del TLB, infatti ogni processo ha il suo TLB e ogni volta che si effettua un process switch si deve anche cancellare il PLB del processo spostato in memoria secondaria. 

***NON HO CAPITO SE OGNI PROCESSO HA IL SUO TLB O SE ESISTE UN TLP UNICO CHE é RESETTATO AD OGNI PROCESS SWITCH***



[^1]:Insieme delle pagine di un processo che sono presenti in memoria principale
[^2]:Interrupt generato quando si prova ad accedere ad una pagina non presente nella memoria principale
[^3]:il registro *Page Table Ptr* contiene un puntatore all'inizio della tabella delle pagine.

