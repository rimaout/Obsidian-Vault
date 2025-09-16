---
type: Uni Note
class: "[[Basi di Dati 1 (class)]]"
academic year: 2024/2025
related:
completed: false
created: 2025-01-24T14:14
updated: 2025-09-16T18:27
---

---
## Introduzione

In un [[Introduzione alle Basi di Dati#BDMS|DBMS]] la principale risorsa a cui i programmi accedono in modo concorrente è la base di dati (BD).

Se sulla BD vengono effettuate **solo letture** (la BD non viene mai modificata), l’*accesso concorrente non crea problemi*.

Se sulla BD vengono effettuate **anche scritture** (la BD viene modificata), l’accesso concorrente può *creare problemi e quindi deve essere controllato*.

---
## Transazione

Una transazione è esecuzione di una parte di un programma che rappresenta un’*unità logica di accesso o modifica* del contenuto della base di dati. 

Una transazione è composta da una *serie ordinata di operazioni*, il cui ordine di esecuzione deve essere rispettato.

##### Proprietà delle Transazioni

Perché le transazioni operino in modo corretto sui dati è necessario che i meccanismi che le implementano soddisfino le proprietà **ACID**:
- **Atomicity** -> Atomicità
- **Consistency** -> Consistenza
- **Isolation** -> Isolamento
- **Durability** -> Durabilità

>[!note]- Atomicità 
>
>Indica che la transazione deve essere ***in-divisibile***, ovvero la sua esecuzione deve essere o *totale* o *nulla*.
>
>Quindi nel caso una transazione dovesse fallire deve essere effettuato un rollback di tutte le modifiche effettuate alla base di dati. Ed in particolare devono essere annullate anche tutte le altre transazioni che hanno utilizzato le modifiche effettuate dalla transazione fallita.

>[!note]- Consistenza
>
>Indica che iniziata una transazione il database si trova in uno stato consistente e quando la transazione termina il database deve essere in un altro stato consistente. 
>
 >>***Stato Consistente*** significa tutti i dati nella base di dati devono rispettare i vincoli di integrità.
 
>[!note]- Isolamento
> 
> Indica che ogni transazione deve essere eseguita in modo isolato e indipendente dalle altre transazioni, l'eventuale fallimento di una transazione non deve interferire con le altre transazioni in esecuzione.
> 
> L’esito di un insieme di transazioni quindi non deve dipendere dall’ordine in cui le eseguo, ovviamente posso ottenere risultati diversi ma l’importante è che non falliscano presa una loro permutazione qualsiasi.

>[!note]- Durabilità (o persistenza)
>Si riferisce al fatto che una transazione dopo aver scritto i suoi risultati sulla base, questi non devono essere persi, per assicurarsi questo vengono scritti anche dei *log* su tutte le operazioni eseguite sul BD.

---
## Schedule

Uno schedule (piano di esecuzione) di un insieme di transazioni (`T`) è un ordinamento delle operazioni delle transizioni (in `T`), che *conserva l’ordine* che le operazioni hanno all’intero delle singole transazioni.

>[!example] Esempio
>
>Se l’operazione O1 precede l’operazione O2 in una transazione allora sarà così in ogni schedule dove compare questa transazione, ovviamente fra loro due potrebbero comparire operazioni di altre transazioni.

### Schedule Seriale

È uno schedule che corrisponde ad una esecuzione sequenziale delle transazioni queste non vengono quindi interrotte e vengono eseguite una per volta per intero.

>[!note] Schedule Coretto
>
>Pertanto tutti gli schedule seriali sono corretti e uno schedule non seriale è corretto se è serializzabile, cioè se è “equivalente” ad uno schedule seriale.

>[!note] Schedule Errato
>
>Definiamo uno schedule errato quando i valori prodotti non sono quelli che si avrebbero se le due transazioni fossero eseguite in modo sequenziale.

### Serializzabilità

Come abbiamo detto uno schedule è serializzabile se "equivalente" a uno schedule seriale, ma cosa significa "equivalente"?

>[!note] Equivalenza
>Due schedule si dicono equivalenti se restittuiscono valori sono uguali per ogni possibile input.
>
>Questa caratteristica potrebbe essere testata sfruttando le proprietà algebriche delle operazioni ma richiederebbe tempo esponenziale.
>
>Quindi si utilizza la *definizione più restrittiva*, ovvero due schedule si dicono equivalenti sei i loro *valori* sono prodotti dalla *stessa sequenza di operazioni* (controllo che può essere fatto in tempo polinomiale).

>[!note] Testare la serializzabilità
>In realtà *testare* la serializzabile, ovvero controllare che uno *schedule* abbia *stessa sequenza di operazioni* della sua versione seriale è molto complicato:
>- È *difficile stabilire* quando uno schedule *comincia o finisce*
>- È *impossibile determinare* in *anticipo* in che *ordine* verranno eseguite le *operazioni* dato che questo dipende dal carico del sistema, l’ordine in cui queste vengono inviate e la loro priorità
>
>Inoltre se eseguiamo uno schedule e poi testando la serializzabilità notiamo che non è serializzabile allora dovremmo annullare i suoi effetti.

>[!note] Protocolli che garantiscono serializzabilità
>
>Quindi il metodo che si usa non è testare la serializzabilità ma usare protocolli che la garantiscono, eliminando la necessità di dover testare gli schedule ogni volta. 
>
>Facciamo questo **imponendo dei protocolli** alle transazioni come [[#Locking]] e [[#Timestamp]].

## Item

Tutte le tecniche per la gestione della concorrenza richiedono che la base di dati sia partizionata in **item**, cioè in unità a cui l’accesso è controllato.

Le dimensioni degli item usate da un sistema sono dette la sua granularità. Una granularità grande permette una gestione efficiente della concorrenza; una piccola granularità può invece sovraccaricare il sistema, ma consente l’esecuzione concorrente di molte transazioni.

>***Esempi:*** La granularità va dal singolo campo ad un’intera tabella o oltre.

## Locking

Ad ogni item è associata una variabile che ne descrive lo stato rispetto alle operazioni che possono essere eseguite su di lui, la variabile assume due valori nel caso di **lock binario**:
- *Locked*: L’item è in uso da una transazione e non può essere utilizzato da altre
- *Unlocked*: È possibile utilizzare l’item per svolgere operazioni su di esso.

Il lock quindi agisce da **primitiva di sincronizzazione**. 

Il lock binario, fa uso di due operazioni:
- `lock(X)` per richiedere l’accesso ad un item `X`
- `unlock(X)` per rilasciare l’item `X`

>[!note] Verifica equivalenza
>
>Il concetto di equivalenza degli schedule cambia in base al protocollo di locking adottato. In questo caso vedremo il **concetto di equivalenza** associato al lock binario.
>
>***Modello*** - per prima cosa utilizziamo un modello delle transazioni che considera soltanto le operazioni rilevanti ovvero gli accessi che nel nostro caso sono soltanto le operazioni di _lock e unlock_, dove ogni _lock(X)_ implica la lettura di _X_ mentre un _unlock(X)_ implica la scrittura di _X_.
>
>***Funzioni*** - associamo ad ogni *unlock* una funzione, diversa dagli altri unlock, che prende come input tutti gli item letti fino ad ora dalla transazione prima di quell’unlock (se l'item in input è stato modificato da un altra transazione dello stesso schedule allora in input prende la funzione associata all'unlock di quella modifica).
>
>Diciamo che schedule sono **equivalenti** quando le formule finali per ciascun item sono uguali.
>
>>[!example]- Esempio
>>
>>Consideriamo le due transazioni:
>>
>>![[Pasted image 20250916131804.png|800]]
>>
>>E lo schedule:
>>
>>![[Pasted image 20250916131820.png|900]]
>>
>>Otteniamo come valore finale di X: $f_{4}​(f_{1}​(X_{0}​),Y_{0}​)$, `Y` per ora non ci interessa.
>>
>>In questo caso abbiamo due possibili schedule seriali quindi dobbiamo confrontare il valore finale di `X` con entrambi:
>>
>>![[Pasted image 20250916131927.png|900]]
>>
>>In questo caso abbiamo come valore finale di `X`: $f_{4}​(f_{1}​(X_{0}​),fw_{2}(X_{0}​,Y_{0}​))$ che è diverso dallo schedule iniziale, proviamo a controllare l’altro schedule seriale:
>>
>>![[Pasted image 20250916132022.png|900]]
>>
>>Questo scrive come valore finale di `X`: $f_{1}​(f_{4}​(X_{0}​,Y_{0}​))$.
>>
>>Quindi lo schedule preso inizialmente non è serializzabile dato che non è equivalente ad uno schedule seriale.

### Testare Serializzabilità (grafo di serializzazione)

Dato uno schedule `S` creiamo un grafo diretto `G`, **grafo di serializzazione** dove:
- i *nodi* sono le transazioni
- Gli *archi* vanno da una transazione `Ti`​ ad una transazione `Tj`​ e hanno etichetta `X` (item) se in `S` la transazione `Ti`​ esegue un `unlock(X)` e `Tj`​ esegue il successivo `lock(X)`.

Lo schedule `s` è ***serializzabile*** se il suo grafo di serializzazione `G` **non ha ciclli**.

>***Nota:*** Attenzione! Non un `lock(X)` successivo qualsiasi, ma il successivo ovvero il primo `lock(X)` immediatamente dopo a quel unlock.

>[!example]- Esempio
>
>Prendiamo lo schedule:
>
>![[Pasted image 20250916151609.png|500]]
>
>Che avrà come grafo:
>
>![[Pasted image 20250916152910.png|400]]
>
>E non è serializzabile dato che ha un ciclo.

>[!note] Teo1: Ordinamento Topologico
>
>Preso il grafo, ogni possibile [[Ordinamento Topologico - Grafi|ordinamento topologico]] è uno schedule serializzabile equivalente a `S`.
>
>**Teorema:** Uno schedule `S` è serializzabile se e solo se il suo grafo di serializzazione è aciclico.

### Protocollo di Locking a due Fasi

Una transazione si dice **a due fasi** se:
- Prima effettua tutte le operazioni di lock (*fase di locking*)
- Poi tutte le operazioni di unlock (fase di *unlocking*)

Quindi una volta effettuato un unlock la transazione è terminata, e non è più possibile effettuare altri lock.

>[!note] Teo2: lock due fasi = schedule serializzabile
>
>Sia `T` un insieme di transazioni, se *ogni transazione* in `T` è **a due fasi** allora *ogni schedule* di `T` è **serializzabile**.
>
>---
>
>**Dimostrazione:**
>
>Sia `T` un insieme di transazioni tutte a due fasi, e `S` uno schedule di `T`.
>
>Supponiamo per assurdo, che `S` non sia serializzabile.
>
>Per il Teorema 1, il grafo di serializzazione `G` di `S` contiene un ciclo `T1,T2,...,Tk,T1`, ciò significa che per ogni `i = 1,...,k-1`:
>- la transazione $T_{i+1}$ effettua un’operazione di lock, su un item su cui $T_{i}$ ha effettuato un’operazione di unlock.
>  
>![[Pasted image 20250916175643.png|400]]
>
>Questo però implica anche che:
> - $T_{1}$ effettua un `unlock` e che $T_{2}$ effettua un `lock` su un item liberato da $T_{1}$
> - $T_{k}$ effettua un `unlock` e che $T_{1}$ effettua un `lock` su un item liberato da $T_{k}$
>   
>Ma questa è una contraddizione dato che `T1` effettua un’operazione di *lock* dopo aver effettuato un’operazione di *unlock* e quindi `T1` **non è a due fasi** (contraddizione).

>[!note] Nota
> 
> Se uno schedule con tutte transazioni non a due fasi non è detto che non sia serializzabile, ma se ne abbiamo anche solo una transazione a due fasi esisterà sempre alemeno una permutazione dello schedule non serializzabile.

### Deadlock e livelock

In un *sistema che utilizza i lock* per il controllo della concorrenza si possono verificare delle situazioni anomale note con il nome di deadlock e livelock.

>[!note] Deadlock
>
>Un deadlock si verifica quando ogni transazione in un insieme T è in attesa di ottenere un lock su un item sul quale qualche altra transazione in T mantiene un lock.
>
>Possiamo verificare il sussistere di una situazione di stallo si mantiene il **grafo di attesa**, dove:
>- I nodi sono le transazioni
>- Gli archi vanno da una transazione `T1` ad una `T2` se la `T1` è in attesa di ottenere un lock su un item sul quale `T2` mantiene un lock.
>
>Se nel grafo c’è un ciclo si verificherà una situazione di stallo che coinvolge le transazioni nel ciclo.
>
>![[Pasted image 20250916175402.png|400]]
>
>>***Soluzione:*** dobbiamo necessariamente effettuare un [[#^7032b7|Abort]] di una delle transazioni coinvolte nello stallo e farla ripartire.

>[!note] Livelock
>
>Un livelock si verifica quando una transazione aspetta indefinitamente che gli venga garantito un `lock` su un certo item.
>
>>***Soluzione:*** possiamo usare una strategia **first came-first served** oppure eseguendo le transazioni in base alla loro **priorità** e aumentando la priorità di una transazione in base al tempo in cui rimane in attesa.

## Definizioni Utili

>[!note] Abort di una Transazione

^7032b7

>[!note] Punto di Commit

>[!note] Dati Sporchi

>[!note] Rollback a Cascata

## Timestamp



## Problemi di Esecuzione

Vediamo a sinistra due transizioni `T1`, `T2` e a destra un loro possibile schedule.

![[Screenshot 2025-01-19 at 21.07.58.png|500]]

