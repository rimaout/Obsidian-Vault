---
type: Uni Note
class: "[[Basi di Dati 1 (class)]]"
academic year: 2024/2025
related:
  - "[[Basi di Dati 1 (class)]]"
completed: true
created: 2024-12-12T13:21
updated: 2025-03-24T12:27
---
## Introduzione

Quando le ***chiavi ammettono un ordine***, è più conveniente utilizzare un organizzazione fisica che tenga conto di questa caratteristica dei dati.

>[!note] Ordinamenti
>La maggior parte dei data type hanno un ordinamento
>- Valori numerici per confronto
>- Stringhe ordine lessicografico
>
>Se abbiamo dati composti da campi multipli, si ordina il primo campo, poi il secondo e cosi via (oss: l'ordinamento lessicografo si comporta allo stesso modo in cui i vari simboli rappresentano i campi)
>
>>[!warning]- Algoritmo di Ordinamento
>>
>>Le condizioni appena viste sono equivalenti al seguente algoritmo:
>>- Si pone n=1
>>- Si confrontano i simboli nella posizione n-esima della stringa:
>>    - Se una delle due non possiede l’elemento n-esimo allora è minore dell’altra e terminiamo
>>    - Se entrambe le stringhe non possiedono l’elemento n-esimo allora sono uguali e l’algoritmo termina
>>    - Se i simboli sono uguali si passa alla posizione successiva
>>    - Se questi sono diversi, il loro ordine è l’ordine delle stringhe

---
## File con Indice Sparso

Un esempio di file and indice sparso può essere un file **ISAM** (Indexed Sequential Access Method)

Questa struttura è composta da due file: 
- [[#^e2d6da|File Principale]]
- [[#^b0976d|File Indice]]

>[!note] File Principale
>
>In questo file i record sono ordinato in base alle chiave, dalla più piccola alla più grande. 
>
>>***oss:*** È importante lasciare dello spazio libero in ogni blocco, ad esempio 20%,  per permettere di inserire nuovi elementi in futuro.

^e2d6da

>[!note] File Indice
>
>Il file indice contiene un record per ogni blocco del file principale, questi record sono composti da due campi:
>
>1. un *puntatore* `p` ad un blocco del file indice (indirizzo del blocco)
>2. un valore `v` che *ricopre* tutte le *chiavi* presenti nel blocco puntato da `p`
>
>Questo a due implicazioni:
>- `v` deve essere *minore uguale* di tutte le chiavi presenti nel blocco puntato da `p` 
>- tutte le chiavi presenti nel blocco precedente a `p` devo essere *inferiori* a `v`
>   
>Anche i ***record*** del file indice sono ***ordinati*** dal più piccolo al più grande, utilizzando come valore di ordinamento la chiave.
>
>![[3. MOCS/Uni MOC/archive/attachments/Pasted image 20241220150200.png|450]]
>
>>**Da Sapere:**
>>- $-\infty$ è una convenzione per la chiave del primo record del file indce. 
>>- È importante lasciare dello spazio libero in ogni blocco, ad esempio 20%,  per permettere di inserire nuovi elementi in futuro.
>>- Solitamente questo file ha una dimensione tale possa essere mantenuto tutto in memoria principale

^b0976d
## Creazione dell'Indice

Il file indice viene creato nel modo seguente. Per ogni blocco del file principale viene creata
una coppia costituita dal valore della chiave del primo record nel blocco e dall’indirizzo del
blocco; l’unica eccezione è rappresentata dal primo blocco per il quale viene preso anziché
il valore della chiave del primo record, un valore (denotato con $-\infty$) che è più piccolo di
qualsiasi valore che può essere assunto dalla chiave.

---
## Accesso al File Principale

Per accedere ad un record del file principale con chiave `k` occorre ricercare nel file indice il record con il più grande valore `v` che ricopre `k`, cioè tale che:
- `v <= k`

Questo significa che `v` deve rispettare una tra queste due condizioni:
- o `v` la chiave dell l'ultimo il record del file indice
- oppure la chiave del record successivo (`v'`) deve essere tale che `k < v'`
  
Una volta trovato il *record del file indice* con valore `v` utilizziamo il suo puntatore per ottenere il blocco del file principale. Ora è possibile ricercare nel blocco il record con chiave `k`.

>[!example]- Esempio
>
>![[3. MOCS/Uni MOC/archive/attachments/Pasted image 20241220150200.png|450]]
>
>Ad esempio il record del file principale con chiave `090` deve trovarsi nel blocco del blocco che ha come chiave del record più piccola `031`, dato che:
>- il blocco precedente ha come chiave più piccola `003` 
>- e tutti i blocchi successivi hanno record chiavi superiori o uguali a `101` 
>
>Oppure il record con chiave `234` deve trovarsi nell’ultimo blocco del file principale dato che nei precedenti i valori della chiave sono minori `220`.

### Ricerca su file indice

>[!note] Ricerca Binaria
>
>Dato che il file indice è ordinato in base ai valori, la ricerca di un valore `v` del indice che ricopre una chiava `k` del file principale può essere effettuata tramite la ricerca binaria, sui blocchi del file indice.
>
>Definiamo i blocchi del file indice con $B_{1}, B_{2}, \dots, B_{n}$
>
>Si fa un accesso al blocco $B_{\lceil n / 2 \rceil}$ e si confronta il valore `v` del primo record del blocco con `k` :
>
>- Se `k = v` abbiamo finito
>- Se `k < v` allora si ripete il procedimento sui blocchi da $B_{1}$ a $B_{\lceil n /2 \rceil -1}$​
>- Se `k > v` allora si ripete il procedimento sui blocchi da $B_{\lceil n /2 \rceil}$ $B_{n}$ (ricontrolliamo anche questo blocco dato che prima abbiamo controllato solo la prima chiave e non il resto del blocco)
>
>Ci si ferma quando troviamo `K = V` oppure quando lo spazio di ricerca è ridotto ad un unico blocco, a questo punto si scansiona il blocco per trovare un valore nei record che ricopre `k`. 
>
>Nel caso peggiore dopo $\lceil \log_{2}n \rceil$ accessi a memoria per la ricerca nel indice`+ 1` accesso al blocco trovato.

>[!note] Ricerca per Interpolazione
>
>Questo metodo di ricerca è utile quando si conosce la distribuzione dei valori della chiave. A differenza della ricerca binaria, che divide sempre l'intervallo a metà, la ricerca per interpolazione cerca di stimare dove potrebbe trovarsi il valore cercato in base alla distribuzione dei dati.
>
>**Funzione f:** La funzione `f(v1, v2, v3)` è fondamentale per la ricerca per interpolazione. Essa calcola una posizione stimata di `v1` all'interno dell intervallo `[v2, v3]`:
>- `v1`: il valore che stai cercando.
>- `v2`: il valore della chiave dell'inizio dell'intervallo
>- `v3`: il valore della chiave della fine dell'intervallo
>
>La funzione restituisce un indice `i` che indica in quale blocco `Bi` potrebbe trovarsi `v1`.
>
>**Procedura Ricerca:** 
>
>Definiamo i blocchi del file indice con $B_{1}, B_{2}, \dots, B_{n}$ e `k` come la chiave del record del file principale da trovare.
>
>Per effettuare la ricerca per interpolazione del valore `k` tra il blocco `B1` e `Bn`, prima di tutto utilizziamo `f(v1, v2, v3`) con:
>- `v1` = `k`
>- `v2` = la chiave del primo record contenuto in `B1`
>- `v3` = la chiave del primo record contenuto in `Bn` 
>
>Il risultato della funzione è un indice `i` di un blocco (`Bi`), ora confrontiamo il risultato con `k`:
>- se `k` è minore del valore della chiave nel primo record di `Bi`, si ripete il procedimento sui blocchi precedenti  ovvero su $B_{1}, B_{2}, \dots, B_{i}$
>- Se `k` è maggiore del valore della chiave nel primo record di `Bi`, si ripete il procedimento sui blocchi successivi, ovvero su $B_{i}, B_{i+1}, \dots , B_{n}$
>
>Questo processo continua fino a quando non si restringe la ricerca a un unico blocco, a questo punto si scansiona il blocco per trovare un valore nei record che ricopre `k`.
>
>**Costo:** È stato calcolato che la ricerca per interpolazione ha una costo sotto forma di accessi a memoria di circa  $1 + \log_2 \log_2 n$ dove $n$ è il numero di blocchi del file indice.
>
>>***Osservazioni:*** Questo tecnica può essere utilizzata soltanto se si conosce una funzione `f` che descrive la distribuzione dei valori, e questo è particolarmente difficile, ed inoltre questa tecnica non è compatibile con utilizzi che alterano la composizione dei dati nel tempo. 

---
## Inserimento

Per inserire un nuovo record con chiave `k` all interno del file principale, prima di tutto dobbiamo ricercare in quale blocco `Bi` del file principale va in inserito il nuovo record. Per questo possiamo effettuare una ricerca.

Se lo **spazio** nel blocco $B_{i}$ è **sufficiente** allora il record viene inserito in modo tale da rispettare l’ordinamento (quindi spostando eventualmente record con chiave maggiore).

Se lo **spazio** nel blocco $B_{i}$ é **in-sufficiente** allora possiamo usare 3 strategie:

***1.*** se nel blocco successivo ($B_{i+1}$) *c'è spazio* allora spostiamo in $B_{i+1}$ il più grande record presente in $B_{i}$ (tenendo in considerazione anche il nuovo record). Il record spostato diventa il primo record di $B_{i+1}$ e, pertanto, il record del file indice che contiene il puntatore a $B_{i+1}$ deve essere modificato con il nuovo valore.

***2.*** se nel il blocco successivo ($B_{i+1}$) *non c'è spazio* o non esiste ($B_{i}$ è l'ultimo blocco) e nel blocco precedente ($B_{i-1}$) *c'è spazio*, allora spostiamo in $B_{i-1}$ il piccolo record presente in $B_{i}$. Il record del file indice che contiene il puntatore a $B_{i}$ deve essere modificato con il nuovo valore.

***3.*** se nel il blocco successivo ($B_{i+1}$) *non c'è spazio* o non esiste ($B_{i}$ è l'ultimo blocco) e nel blocco precedente ($B_{i-1}$) *non c'è spazio* o non esiste ($B_{i}$ è il primo blocco) allora è necessario richiedere un nuovo blocco che seguirà $B_{i}$ e ripartire i record di $B_{i}$ tra $B_{i}$ e il nuovo blocco; occorre anche inserire nel file indice il record relativo al nuovo blocco.

---
## Cancellazione

Per ***cancellare un record dal file principale***, occorre:

1. Ricercare il record
2. Cancellarlo
3. Spostare i record nel blocco in modo da recuperare lo spazio lasciato libero
4. Modificare i bit di "usato/non usato" nell'intestazione del blocco

Se il *record cancellato* è il **primo record del blocco**, occorre:

* Modificare nel file indice il record relativo al blocco

Se il *record cancellato* era l'**unico record del blocco**, occorre:

* Restituire il blocco al sistema
* Cancellare nel file indice il record relativo al blocco

In ogni caso, occorrerà modificare i bit di "usato/non usato" nelle intestazioni dei blocchi coinvolti.

---
## Modifica

La procedura di modifica di un record del file indice varia in base a se dobbiamo modificare campi che coinvolgono la chiave oppure no.

Se la modifica riguarda **campi non chiave** allora dobbiamo:
- Il record viene semplicemente modificato

Se la modifica riguarda **campi chiave** allora dobbiamo:
- Cancellare il record
- Inserire un nuovo record nel file principale con i campi modificati

---

## File principale con record puntati

**Inizializzazione:**

La fase di inizializzazione non differisce dal caso precedente, salvo che è preferibile lasciare più spazio libero nei blocchi per successivi inserimenti. 

Ciò è dovuto al fatto che i record sono puntati e non possono essere spostati per mantenere l'ordinamento quando si inseriscono nuovi record.

**Inserimento di nuovi record:**

Se non c'è spazio sufficiente in un blocco `B` per l'inserimento di un nuovo record, occorre richiedere al sistema un nuovo blocco che viene collegato a `B` tramite un puntatore. 

In tal modo, ogni record del file indice punta al primo blocco di un bucket e il file indice non viene mai modificato (a meno che le dimensioni dei bucket non siano diventate tali da richiedere una riorganizzazione dell'intero file).

**Ricerca di un record:**

La ricerca di un record con chiave `v` richiede la ricerca sul file indice di un valore della chiave che ricopre `v` e quindi la scansione del bucket corrispondente.

**Cancellazione di un record:**

La cancellazione di un record richiede la ricerca del record e quindi la modifica dei bit di cancellazione nell'intestazione del blocco.

**Modifica di un record:**

La modifica di un record richiede prima di tutto una *ricerca* del record poi il procedimento cambia si deve modificare un campo chiave oppure no.


Se la modifica ***non coinvolge*** campi della ***chiave***, il record viene modificato e il blocco riscritto.

Se la modifica ***coinvolge*** campi delle ***chiave*** allora equivale ad una *cancellazione* seguita da un *inserimento*.  In quest'ultimo caso, non è sufficiente modificare il bit di cancellazione del record cancellato, ma è necessario inserire in esso un puntatore al nuovo record inserito in modo che questo sia raggiungibile da qualsiasi record che contenga un puntatore al record cancellato.

**Ordinamento del file principale:**

Poiché non è possibile mantenere il file principale ordinato, se si vuole avere la possibilità di esaminare il file seguendo l'ordinamento della chiave, occorre inserire in ogni record un puntatore al record successivo nell'ordinamento.

Ecco le informazioni riguardanti i file ISAM con record puntati, riformattate per una maggiore leggibilità:

**Caratteristiche dei record puntati**

* **Immobilità dei record**: una volta inseriti, i record del file principale non possono essere spostati per mantenere l'ordinamento. Ciò significa che l'ordinamento stretto dei record è valido solo all'inizializzazione.
* **Stabilità dei record indice**: a differenza dell'ISAM classico, i record dei blocchi indice non vengono mai modificati. Ciò significa che la ripartizione degli intervalli delle chiavi rimane valida.

**Gestione degli intervalli delle chiavi**

* **Condizione di validità**: se un record indice punta ad un'area di dati con valori di chiave comprese tra `k1` e `k2`, questa condizione deve rimanere valida.
* **Gestione degli overflow**: se il blocco originario si riempie e arrivano nuovi record con valori di chiave compresi sempre tra `k1` e `k2`, dobbiamo allocare un nuovo blocco che sarà linkato al blocco originario. Ciò crea una lista di blocchi di overflow che partono da quello originario, dove ognuno punta al successivo.

In sintesi, i record puntati non possono essere spostati per mantenere l'ordinamento, ma la ripartizione degli intervalli delle chiavi rimane valida. Quando si verificano degli overflow, si creano nuovi blocchi che sono linkati al blocco originario, creando una lista di blocchi di overflow.

![[Pasted image 20250123184731.png|800]]