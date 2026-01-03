---
type: Uni Note
class:
  - "[[Interazione Uomo Macchina (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-12-17T16:10
updated: 2025-12-18T10:13
---
## Introduzione

Le valutazioni vengono effettuate su degli artefatti (artifact) e ne valutano sia il design che l'implementazione.

>***Artifact***: simulazioni, prototipi, full implementations

Sono molto utili se applicate a tutti gli stage del design life cycle e determinano:
- to assess extent of *system functionality*
- to assess eﬀect of *interface on user*
- to *identify specific problems*

>[!note] Utenti
>Le valutazioni sono effettuati attraverso degli **utenti**, che dovrebbero:
>- rappresentare il target degli utenti dello studio
>- dovrebbero avere esperienza simili (omogenei)
>- avere conoscenze nel dominio di studio
>- essere almeno 3/5 utenti

>[!note] Scenario e Task
>
>Lo **scenario** descrive una situazione potenzialmente reale nella quale si immedesimano i partecipanti alla valutazione
>- permette di individuare: utenti, azioni, strumenti da usare e contesti
>
>I **task** sono i singoli compiti che si richiede di svolgere ai partecipanti

## Stili di Valutazione
- [[#Laboratory Studies]]
- [[#Field Studies]]

### Laboratory Studies

Appropriate if system location is dangerous or impractical

***Positives:***
- specialist equipment available
- uninterrupted environment

***Negatives:***
- lack of context
- diﬃcult to observe several users cooperating

![[Pasted image 20251217175925.png|500]]

![[Pasted image 20251217180032.png|500]]

### Field Studies

Appropriate where context is crucial for longitudinal studies.

***Positives:***
- natural environment
- context retained (though observation may alter it)
- longitudinal studies possible

***Negatives:***
- distractions
- noise

![[Pasted image 20251217180332.png|500]]

## Observational Methods

>[!note] Think Aloud
>
>***Characteristics***:
>- user observed performing task
>- user asked to describe what he is doing and why, what he thinks is happening etc
>
>***Positives***:
>- simplicity - requires little expertise
>- can provide useful insight
>- can show how system is actually used
>
>***Negatives***:
>- subjective
>- selective
>- act of describing may alter task performance

^8f6847

>[!note] Cooperative evaluation
>
>It's a variation of [[#^8f6847|Think Aloud Method]] where the *user collaborates in evaluation*:
>- both user and evaluator can ask each other questions throughout
>
>Additional ***advantages***:
>- less constrained and easier to use
>- user is encouraged to criticize system
>- clarification possible 

>[!note] Protocol analysis
>
>`protocol = recording of evaluation session`
>
>There are different ways to "write" a protocol:
>- *paper and pencil*: cheap, limited to writing speed
>- *audio*: good for think aloud, diﬃcult to match with other protocols
>- *video*: accurate and realistic, needs special equipment, obtrusive
>- *computer logging*: automatic and unobtrusive, large amounts of data diﬃcult to analyze
>- *user notebooks*: coarse and subjective, useful insights, good for longitudinal studies
>  
>In practice a mix of these techniques is used.

>[!note] Post-task walkthroughs
>
>Tecnica utilizzata nella ricerca per raccogliere informazioni aggiuntive dai partecipanti dopo che hanno completato un compito. 
>
>Prevede di riprodurre la trascrizione del compito al partecipante e chiedergli di commentare le proprie azioni e decisioni.
>
>**Tipi di de-briefing:**
>- ***Immediato***: il de-briefing viene condotto subito dopo il compito, quando i dettagli sono ancora freschi nella mente del partecipante
>- ***Ritardato***: il de-briefing viene condotto dopo un certo periodo di tempo, permettendo al valutatore di riflettere sulle domande da chiedere al partecipante.
>
>**Quando utilizzare il de-briefing:**
>- Quando non è possibile utilizzare la tecnica del "think aloud" (pensare ad alta voce)
>- Quando si desidera raccogliere informazioni aggiuntive sui processi decisionali dei partecipanti

## Misurazioni

I metodi di valutazione discussi sono soggettivi e dipendono dalle conoscenze e dalle capacità del valutatore. Il valutatore deve essere in grado di riconoscere i problemi e comprendere cosa fa l'utente.

**Problemi dei metodi di valutazione:**

- **Bias del valutatore** (evaluator bias): può essere attenuato utilizzando più valutatori
- **Risposta soggettiva dell'utente**: anche la risposta dell'utente può essere soggettiva

>[!note] Misure qualitative
>
>- I metodi discussi producono misure qualitative, ovvero non numeriche
>- Queste misure possono rivelare dettagli che non possono essere determinati da misure numeriche
>- I metodi soggettivi generalmente portano a misure qualitative

In generale, è importante essere consapevoli delle limitazioni dei metodi di valutazione e cercare di mitigare i bias e le soggettività per ottenere risultati più affidabili.

## Valutazione Sperimentale

La valutazione sperimentale è un metodo di valutazione che consiste nell'effettuare un esperimento per studiare degli aspetti specifici del comportamento interattivo.


>[!note] Fattori Sperimentali
>
>- **Soggetti**: chi sono i partecipanti, rappresentativi e sufficienti?
>- **Variabili**: cosa modificare e misurare?
>- **Ipotesi**: cosa si vuole dimostrare (un'idea provvisoria il cui valore dev'essere accertato)
>- **Progettazione sperimentale**: come si effettuerà la valutazione?

>[!note] Variabili
>
>- **Variabile indipendente (IV)**: caratteristica modificata per produrre condizioni diverse (ad esempio, stile dell'interfaccia, numero di elementi del menu)
>- **Variabile dipendente (DV)**: caratteristica misurata nell'esperimento (ad esempio, tempo impiegato, numero di errori)

>[!note] Ipotesi
>
>- **Ipotesi alternativa**: previsione che una variazione della IV causerà una differenza nella DV (ad esempio, "la frequenza degli errori aumenterà al diminuire della dimensione del carattere")
>- **Ipotesi nulla**: afferma che non ci sarà differenza nella DV (ad esempio, "nessun cambiamento con la dimensione del carattere")

>[!note] Progettazione Sperimentale
>
>- Scegliere l'ipotesi
>- Scegliere le variabili dipendenti e indipendenti (le variabili indipendenti devono essere le più semplici possibili)
>- Scegliere i partecipanti
>- Scegliere il metodo sperimentale: between subjects o within subjects

>[!note] Condizioni
>- **Condizione di controllo**: condizione di base per confrontare i risultati
>- **Condizione sperimentale**: condizione in cui solo una variabile indipendente viene modificata rispetto alla condizione di controllo

>[!note] Metodi sperimentali
>
>**Between subjects**: ogni partecipante viene assegnato a una sola condizione e svolge il test una volta sola.
>- *Positives:* non risente del “trasferimento dell’apprendimento”
>- *Negatives:* 
>	- sono richiesti più partecipanti
>	- variazioni tra gli utenti possono alterare il risultato della valutazione
>
>**Within subjects**: ogni partecipante viene assegnato a tutte le condizioni che vengono analizzate singolarmente svolgendo il test più volte ogni volta con una condizione diversa.
>- *Positives:* 
>	- richiede meno partecipanti, quindi è meno costoso
>	-  le diﬀerenze tra gli utenti influenzano di meno la valutazione
>- *Negatives:*
>	- risente del “trasferimento dell’apprendimento”

>[!note] Mitigare il trasferimento dell'apprendimento
>
>**Problema:** si verifica quando un partecipante esegue un compito più volte, con diverse condizioni sperimentali, e apprende qualcosa durante la prima esecuzione del compito che può influenzare le sue prestazioni nelle esecuzioni successive
>
>>***Esempio:*** un partecipante esegue un compito con un'interfaccia utente e poi esegue lo stesso compito con un'altra interfaccia utente, potrebbe aver già imparato alcune cose durante la prima esecuzione del compito che possono aiutarlo a eseguire meglio il compito con la seconda interfaccia utente, anche se la seconda interfaccia utente è diversa dalla prima.
>
>**Mitigazione:**
>- Metà dei partecipanti esegue il test dapprima sotto la condizione di controllo, poi sotto la condizione sperimentale
>- L'altra metà esegue il test dapprima sotto la condizione sperimentale, poi sotto la condizione di controllo

>[!note] Analisi Statistica
>
>- Osservare i dati raccolti (DV)
>- Possibilmente su un grafico
>- Ricerca di outliers
>- Salvare i dati originali (potrebbero essere necessari in seguito)
>
>**Tipi di dati:**
>- variabili discrete o continue
>- variabili continue positive (> 0). Es. tempo impiegato
>- variabili indipendenti tipicamente discrete
>- distribuzione normale della variabile dipendente
>  
>**Risultati:**
>- Se i dati soddisfano la distribuzione normale: test parametrici (tecniche di analisi statistica standard molto robuste)
>- Altrimenti: test non parametrici, tabella di contingenza,…
>- Verifiche d'ipotesi: sì/no al rifiuto dell'ipotesi nulla (ad esempio, "possiamo, al 99%, rifiutare l'ipotesi nulla")

## A/B Testing (esperimento di usabilità)

L' A/B Testing è l'esperimento di usabilità più semplice, consiste nel confrontare due versioni di un prodotto o di un servizio per determinare quale sia più efficace.

Questo tipo di esperimento è comunemente utilizzato per testare piccole modifiche a un prodotto o di un servizio e per determinare se queste modifiche abbiano un impatto significativo sull'esperienza dell'utente.

L'esperimento di usabilità più semplice è caratterizzato da:
- Una sola variabile indipendente con due valori (A e B)
- Due condizioni (A e B)
- Utilizzo di un test statistico (ad esempio test di distribuzione Gaussiana: [t-test](https://it.wikipedia.org/wiki/Test_t)) per confrontare i risultati.

L'obiettivo di questo tipo di esperimento è di determinare se c'è una differenza statisticamente significativa tra le due versioni. Per raggiungere questo obiettivo, i partecipanti vengono assegnati casualmente alle due condizioni e vengono misurate le variabili dipendenti (ad esempio, conversion rate, call-to-action clicks, engagement).

 I vantaggi di questo tipo di esperimento sono:
- Semplicità di progettazione e realizzazione
- Risultati facili da misurare e interpretare
- Possibilità di ottenere risultati chiari e significativi

Tuttavia, ci sono anche alcuni svantaggi:
- Adatto solo al caso di due condizioni diverse
- Difficoltà nel decidere cosa misurare (A e B) in alcuni casi

>[!example] Esempio
>
>![[Screenshot 2025-12-18 at 10.11.05.png|600]]
>
>*Variabili dipendenti*:
>- conversion rate (CVR)
>- call-to-action (CTA) clicks
>- engagement
>
>*Risultato*: CVR nella condizione B è superiore del 6% ad A (in C è inferiore ad A).

