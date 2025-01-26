---
type: Uni Note
class: "[[Basi di Dati 1 (class)]]"
academic year: 2024/2025
related: 
completed: true
created: 2024-11-30T15:34
updated: 2025-01-24T14:14
---
## Introduzione

Un requisito fondamentale di un sistema di gestione di basi di dati è l’efficienza, cioè la
capacità di rispondere alle richieste dell’utente il più rapidamente possibile.

Il **tempo di risposta del sistema** è teoricamente composto da diversi casi:
- tempo di acceso alla memoria secondaria
- tempo di accesso alla memoria principale
- tempo di elaborazione della CPU

Ma i tempi di accesso alla memoria secondaria sono molto più alti rispetto al resto, per questo la valutazione del ***tempo di risposta del sistema*** ad una richiesta dell’utente viene effettuata in termini di *numero di accessi a disco*. 

>[!warning] Assunzione
>Nel nostro caso, per semplicità, assumiamo che il tempo di accesso al disco sia costante ma nel mondo reale i blocchi trasferiti sono memorizza in un buffer, rendendo in alcuni casi molti più rapido l'accesso ai blocchi.
>
>Inoltre il costo di un accesso a disco non è fisso, ma dipende dalla posizione del blocco rispetto all’ultimo blocco tresferito in quanto da ciò dipendono sia lo spostamento della testina da un cilindro all’altro sia la rotazione del disco.

Un disco al momento della formattazione viene diviso in blocchi di dimensione fissa (compresa tra $2^{9}$ e $2^{12}$ byte).

>[!note] Acesso Disco
>
>Per accesso ad un disco si intende il *trasferimento* di un *blocco* da memoria secondaria a memoria principale (lettura di un blocco) o da memoria principale a memoria secondaria (scrittura di un blocco).

>[!note] Unita di misura
>Il [[#Blocco]] è utilizzato sia come *unita di misura* di allocazione che di trasferimento.

---
## Relazioni, Attributi e Tuple

- Una *reazione* (tabella relazionale) corrisponde a [[#File]] di [[#Record]] che hanno tutti lo stesso numero e tipo di campi.
- Ogni *attributo* di una tupla corrisponde a un campo di un [[#Record]].
- Una *tupla* corrisponde ad un [[#Record]]

---
## Record

Un Record non è altro che la rappresentazione fisica di una **tupla**, ovvero un insieme di attributi. 

>[!note] Campi
>Le informazione contenute dal record sono chiamati campi e ci sono due tipi:
>- Attributi della relazione (capi di tipo intero, reale, stringa)
>- puntatori a record
>- Informazioni aggiuntive sul record
>
>Per informazione aggiuntive si intende:
>- alcuni byte possono essere utilizzati per specificare il tipo del record (è necessario quando in uno stesso blocco sono memorizzati record di tipo diverso, ovvero record appartenenti a più file)
>- uno o più byte possono essere utilizzati per specificare la lunghezza del record se il record ha campi a lunghezza variabile
>- bit di “cancellazione” o un bit di “usato/non usato”

>[!note] Puntatore a record
>Un puntatore ad un record è essenzialmente un dato che permette di accedere rapidamente a quel record, e ci sono due principali metodi per rappresentarlo:
>
>**Metodo semplice:** Un puntatore può essere l’indirizzo dell’inizio (primo byte) del record su disco.
>
>**Metodo avanzato:** Puntatore rappresentato da una coppia `b,k` in cui `b` è l’indirizzo del blocco che contiene il record e `k` è il valore di uno o più campi che servono come chiave (attributo chiave) nel file a cui il record appartiene. 
>
>>**oss:** con il metodo avanzato è possibile *spostare il record all’interno del blocco*.

>[!warning] Accesso ai campi 
>Per poter accedere ad un campo contenente un dato è necessario sapere qual è il primo byte del campo all interno del record. il* numero di byte del record che precedono il campo* è detto *offset* del campo.
>
>**Campi di lunghezza fissa:** Se tutti i campi del record hanno lunghezza fissa, l’inizio di ciascun campo sarà sempre ad un numero fisso di byte dall’inizio del record.
>
>**Campi di lunghezza variabile:** Se il record contiene campi a lunghezza variabile allora l’offset di un campo può variare da un record all’altro. In tal caso si possono usare due strategie.
>1. All’inizio di ogni campo c’è un contatore che ne specifica la lunghezza in numero di byte.
>2. All’inizio del record ci sono dei puntatori (qui un puntatore è inteso come l’offset del campo) all’inizio di ciascun campo a lunghezza variabile (tutti i campi a lunghezza fissa precedono quelli a lunghezza variabile).
>   
>![[Pasted image 20241130181929.png|800]]

---
## Blocco

I blocchi sono gli spazzi fisici sul disco in cui vengono salvati i record.

**Importantemente:** posso memorizzare in un certo blocco soltanto un numero intero di record 

>[!note] Informazioni Aggiuntive
>
>Oltre ai record un blocco contiene delle informazioni aggiuntive, come:
>- Puntatori ad alri blocchi
>- record cancellati, record non usati,
>- puntatori a record se il blocco contiene record a lunghezza variabile

>[!warning] Record di lunghezza fissa
>
>Un blocco che contiene solo record di lunghezza fissa è suddiviso in aree (sottoblocchi) di lunghezza fissa ciascuna delle quali può contenere un record. 
>
>Per inserire un record nel blocco basta cercare un area non usata, due metodi:
>1. il bit “usato/non usato” è in ciascun record.
>2. i bit “usato/non usato” in uno o più byte all’inizio del blocco, con "puntatori" a blocchi non usati.
>   
>Il primo metodo è il più lento perché richiede potrebbe richiedere la scansione di tutto il blocco, il secondo "spreca" più spazio avendo informazioni aggiuntive.

>[!warning] Record di lunghezza variabile
>
>Se un blocco contiene record di lunghezza variabile per accedere ai record si possono usare due strategie:
>
>**Metodo 1:** 
>- Si suppone che il primo record abbia inizio dal primo byte del blocco, su ogni record contiene un campo che ne specifica la lunghezza in termini di numero di byte.
>- Per calcolare il byte di inizio di un record si somma all’offset del record precedente la sua lunghezza ed eventualmente si prende il successivo multiplo di 4
>
>**Metodo 2:** All’inizio del blocco è presente una directory contenente i puntatori ai record nel blocco. Poiché il numero di record che possono entrare in un blocco è in questo caso variabile, la directory può essere realizzata in uno dei modi seguenti:
>1. la directory è preceduta da un campo che specifica quanti sono i puntatori nella directory
>2. la directory ha dimensione fissa ed è utilizzato il valore 0 negli spazi che contengono puntatori nulli
>3. la directory è una lista (dimensione variabile) di puntatori e la fine è indicata da uno 0

---
## File

Un file è una tabella relazionale ovvero di tuple (record) che vengono distribuiti su uno o più blocchi.

Le **operazioni elementari** su questi file sono:
- la *ricerca* di uno o più record con un dato valore per la chiave
- l’*inserimento* di un record con un dato valore per la chiave
- la *cancellazione* di uno o più record con un dato valore per la chiave;
- la *modifica* di uno o più record con un dato valore per la chiave.

>[!warning] Osservazione
>
>L’operazione della **ricerca** è alla base di tutte le altre infatti:
>- L'inserimento utilizza la ricerca se vogliamo evitare duplicati
>- La cancellazione richiede la ricerca del record da cancellare
>- La modifica richiede la ricerca del record da cancellare
>  
>
>Il termine **chiave** non va inteso nel senso in cui viene usato nella teoria relazionale, in quanto un valore della chiave non necessariamente identifica univocamente un record nel file.

>[!note] Tipi di File
>Esistono diversi tipi di organizzazione fisica dei file che variano nella velocità di esecuzione delle operazioni elementari:
>- [[File Heap]]
>- [[File Hash]]
>- [[File con Indice]]
>- [[File B-Tree]]