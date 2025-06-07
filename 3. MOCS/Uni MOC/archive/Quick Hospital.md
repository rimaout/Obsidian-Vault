---
type: Uni Note
class: "[[Basi di Dati 2 (class)]]"
academic year: 2024/2025
related: 
completed: false
created: 2025-06-02T11:56
updated: 2025-06-03T13:03
---
## Raffinamento

>[!note] Use Case
>
>- Il sistema QuickHospital è accessibile ai medici, al personale amministrativo e a quelli dell’ufficio prenotazioni.
>- Personale di accettazione --> ricovero di un paziente, dimissione paziente, storico ricoveri, posti letto disponibili 
>- Medico --> calcolare l suo itinerario delle visite
>- Personale di accettazione --> registrazione paziente anche esterno
>- Paziente Esterno --> Richiesta prestazione

>[!note] Operazioni
>
>**Ricovero** - Un paziente può essere ricoverato, in una certa data, solo se una precedente verifica della disponibilità dei posti letto presenti nell’ospedale ha dato esito positivo. Una volta effettuato il ricovero, il paziente ha assegnato un posto letto e una stanza.
>- registrazione ricovero
>- dimissione ricovero
>
>**Ottimizzazione Percorso Medio**: 
>- Inoltre il sistema deve assistere i medici ottimizzando il loro percorso di visite. In particolare, il sistema deve permettere di calcolare, su richiesta di un medico, il suo itineriario delle visite, ovvero un insieme ordinato delle stanze cui accedere (che sono tutte e sole le stanze che ospitano i pazienti che ha in cura).
>- L’ordinamento è dato in primo luogo dal piano delle stanze dei pazienti da visitare, ed in secondo luogo dal settore di appartenenza di tali stanze (entrambi in ordine crescente). I settori sono infatti numerati secondo un criterio di vicinanza topologica.  Pertanto se un dato medico deve visitare le stanze {(7, 4), (7, 1), (1, 3), (1, 1), (3, 4)} dove la prima componente di ognuna è il piano e la seconda il settore, l’itinerario di visita proposto deve essere [(1, 1), (1, 3), (3, 4), (7, 1), (7, 7)]
>  
>**Medici Idonei** - Data una specializzazione `s`, il sistema deve restituire l’insieme dei medici maggiormente idonei a soddisfarla. Il criterio di idoneità è il seguente: se esistono medici con specializzazione primaria pari ad `s`, il risultato è l’insieme di tali medici. Altrimenti, il risultato è l’insieme dei medici che hanno `s` tra le loro specializzazioni secondarie.

1. Requisiti **Persona**:
	- 1.1. Nome
	- 1.2. Cognome
	- 1.3. Data di Nascita

2. Requisiti **Paziente**:
	- 2.1. Persona (v.r. 1)
	- 2.2. Telefono (stringa con caratteri numerici composta da prefisso e suffisso)
	- 2.3. Email (Stinga con formattazione specifica) (univoco)
	- 2.4. Indirizzo Postale (stringa con formattazione specifica) (univoco)
	- Un paziente deve essere o interno o esterno

3. Requisiti **Medici**:
	- 3.1. Persona (v.r. 1)
	- 3.2. Specializzazione Primaria (una) (v.r. 7)
	- 3.3. Specializzazioni Secondarie (v.r. 7)
	- 3.4. Lista dei ricoveri (v.r. 5) (ovvero la lista dei pazienti in cura)

>***oss:*** non si può avere come specializzazione secondarie una che è già primaria (vincolo esterno)

4. Requisiti **Stanza**:
	- 4.1. Posti letto (minimo 1, massimo 8)
	- 4.2. Piano (numero)
	- 4.3. Settore (stringa)
	
5. Requisiti **Ricovero**:
	- 5.1. Paziente Intero
	- 5.2. Data inizio
	- 5.3. Stanza (v.r. 4)
	- 5.4.Un ricovero può essere terminato, in questo caso contiene:
		- 5.4.1 Data dimissione
	
6. Requisiti **Prestazioni**:
	- 6.1. Specializzazione Richiesta (v.r. 7)
	- 6.2. Informazioni Aggiuntive (Stinga)
	- 6.3. Medico
	- 6.4. Paziente Esterno
	- 6.4. Data
	
7. Requisiti **Specializzazione**:
	- 7.1. Nome
## Analisi dei Dati

### Diagrama UML

![[Pasted image 20250603104412.png|1200]]

### Specifiche dei tipi di dato

- `Telefono`- Stringa che segue standard 
- `EMail`- Stringa che segue standard 
- `Indirizzo`- Stringa che segue standard 

### Specifica classi e associazioni

Non essendoci delle operazioni di classe nella mia implementazione non devo fare niente.

>[!warning] Caso Agla
>
>Ad esempio lei invece di memorizzare la data di fine per il ricovero, ha memorizzato la durata e poi utilizza un operazione per determinare la fine.
>
>![[Pasted image 20250603115812.png|400]]
>
>è stato fatto in questo modo, per evitare di dover definire il vincolo esterno (data fine > data inizio)

>***Nota:*** la differenza tra un operazione di classe ed una operazione di use-case è che le operazioni di classi potrebbero essere visti come dei dati, ovvero delle operazioni che una volta chiamate ritornano un valore associato a quella classe. Ad esempio nel progetto Tutubi la classe video ha un operazione `visualizzazioni()` che ritornava il numero di visualizzazioni del video, che può essere derivato del numero di link visualizzazione che al il video. Al contrario l'operazione `visualizza` è un operazione di use-case perché  on ritorna alcun tipo di dato (crea dei link).

### Specifica vincoli esterni

- Dominio: $D = \{ \ \}$
- Funzioni: $F = \{ \ \}$
- Proposizioni: $P = \{\text{Uguale/2},\ \text{Medico/1},\ \text{Specializzazione/1},\ \text{SpecializzazionePrimaria/2},\ \text{SpecializzazioneSecondaria/2} \}$

>[!note] Classe Medico
>
>```
>Idea: non può esistere una specializzazione primaria che è anche secondaria
>
>[V.medico.no_specializzazione_primaria_in_secondaria]
>
>Dato un m:Medico e una sp:Specializzazione tali che partecipano al link (m,sp):specializzazione_primaria, allora non deve esistere una ss:Specializzazione tale che:
>- ss == sp
>- m e ss partecipano al link (m, ss):specializzazione_secondaria
>```
>
>💣💣💣💣💣💣💣💣
>```
>Idea: un medico non può effettuare più prestazioni allo stesso momento
>```

>[!note] Classe Prestazione
>
>```
>Idea: non possono esistere due o più prestazioni per lo stesso paziente allo stesso momento
>
>[V.prestazione.no_più_prestazioni_allo_stesso_momento_per_stesso_paziente]
>
>Dato un pa:paziente, p1:prestazione e una p2:prestazione se:
>- p1 =/= p2
>- esiste link (pa, p1):esterno
>- esiste link (pa, p2):esterno
>  
>Allora p1.data_ora =/= p2.data_ora
 >```

>[!note] Classe Ricovero
>
>```
>Idea: non possono esistere due o più ricoveri (non terminati) per un determinato paziente
>
>[V.Ricovero.un_solo_ricovero_non_terminato_per_paziente]
>Dato un p:paziente e un r1:ricovero se:
>- esiste il link (p,r1):interno
>- r1 non è istanza di ricoveroTerminato 
>
>Allora non deve esistere un r2:ricovero tale che:
>- esiste il link (p,r2):interno
>- r2 non è istanza di ricoveroTerminato
>```

>[!note] Classe RicoveroTerminato
>
>```
>Idea: la fine di un ricovero deve essere dopo l'inizio
>
>[V.RicoveroTerminato.fine_maggiore_inizio]
>Dato un rt:RicoveroTerminato allora il rt.fine > rt.inizio
>```
>
>```
>Idea: non possono esistere due o più ricoveri terminati per lo stesso paziente nello stesso periodo
>
>[V.RicoveroTerminato.no_più_ricoveri_nello_stesso_periodo_per_stessoo_paziente]
>Dati p:paziente, rt1:RicoveroTerminato e rt2:RicoveroTerminato, se:
>- rt1 =/= rt2
>- esiste il link (p, rt1):interno
>- esiste il link (p, rt2):interno
>  
>Allora rt1.fine > rt2.inizio or rt2.fine > rt1.inizio
>```

## Analisi delle funzionalità

### Diagramma Use-Case

### Segnatura operazioni use-case

>***oss:*** ovvero la firma delle operazioni di use-case, quindi `nome(input): output`

### Specifica operazioni use-case

>***oss:*** all'esame non dobbiamo implementare tutte le operazioni di use case, ma soltanto quelle che sono segnate con una sbarra laterale nera.

