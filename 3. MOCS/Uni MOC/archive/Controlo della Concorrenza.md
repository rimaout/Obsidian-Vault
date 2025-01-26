---
type: Uni Note
class: "[[Basi di Dati 1 (class)]]"
academic year: 2024/2025
related: 
completed: false
created: 2025-01-24T14:14
updated: 2025-01-24T15:39
---
## Introduzione

In un [[Introduzione alle Basi di Dati#BDMS|DBMS]] la principale risorsa a cui i programmi accedono in modo concorrente è la base di dati (BD).

Se sulla BD vengono effettuate **solo letture** (la BD non viene mai modificata), l’*accesso concorrente non crea problemi*.

Se sulla BD vengono effettuate **anche scritture** (la BD viene modificata), l’accesso concorrente può *creare problemi e quindi deve essere controllato*.

---
## Transazione

>[!note] Definizione
>L'esecuzione di una parte di un programma che rappresenta un’unità logica di accesso o modifica del contenuto della base di dati. 
>
>Può essere vista come una vera e propria operazione sulla base di dati.

##### Proprietà delle Transazioni

Perché le transazioni operino in modo corretto sui dati è necessario che i meccanismi che le implementano soddisfino le proprietà **ACID**:
- **Atomicity** -> Atomicità
- **Consistency** -> Consistenza
- **Isolation** -> Isolamento
- **Durability** -> Durabilità

L'**atomicità** indica che la transazione deve essere ***in-divisibile*** nella sua esecuzione e la sua esecuzione deve essere o *totale* o *nulla*, non sono ammesse esecuzioni parziali;

La **consistenza** indica che iniziata una transazione il database si trova in uno stato consistente e quando la transazione termina il database deve essere in un altro stato consistente. 

 >***Stato Consistente*** significa che non devono verificarsi contraddizioni (inconsistenza) tra i dati archiviati nel DB.

 L'**isolamento** indica che ogni transazione deve essere eseguita in modo isolato e indipendente dalle altre transazioni, l'eventuale fallimento di una transazione non deve interferire con le altre transazioni in esecuzione.

La **durabilità** (o persistenza) si riferisce al fatto che una transazione dopo aver scritto i suoi risultati sulla base, questi non devono essere persi, per assicurarsi questo vengono scritti anche dei log su tutte le operazioni eseguite sul BD.

---
## Schedule

Uno schedule (piano di esecuzione) di un insieme di transazioni (`T`) è un ordinamento delle operazioni delle transizioni  (in `T`), che *conserva l’ordine* che le operazioni hanno all’intero delle singole transazioni.

>[!example] Esempio
>
>Se l’operazione O1 precede l’operazione O2 in una transazione allora sarà così in ogni schedule dove compare questa transazione, ovviamente fra loro due potrebbero comparire operazioni di altre transazioni.

### Schedule Seriale

È uno schedule ottenuto permutando le transazioni in `T`, questo corrisponde ad una esecuzione sequenziale delle transazioni queste non vengono quindi interrotte e vengono eseguite una per volta per intero.

>[!note] Schedule Accettabile
>
Vedremo più avanti che uno schedule accettabile è uno schedule ovvero equivalente ad uno schedule seriale.

## Problemi di Esecuzione

Vediamo a sinistra due transizioni `T1`, `T2` e a destra un loro possibile schedule.

![[Screenshot 2025-01-19 at 21.07.58.png|500]]

