---
type: Uni Note
class: "[[Basi di Dati 1 (class)]]"
academic year: 2024/2025
related: 
completed: false
created: 2024-11-30T19:23
updated: 2024-12-01T17:56
---
>[!abstract] Related
>- [[Basi di Dati 1 (class)]]

---
## Introduzione

In questo tipo di file non c'è una vera e propria organizzazione dei record, i nuovi record vengono semplicemente inseriti come ultimo record del file.

>[!note] Accesso ai File
>L’accesso al file avviene attraverso una directory che contiene i puntatori ai blocchi, se le dimensioni lo consentono (se la directory entra in un unico blocco), tale directory può essere mantenuta in memoria principale durante l’utilizzo del file; altrimenti saranno necessari ulteriori accessi per portare in memoria principale i necessari blocchi della directory.

>[!info] Pro / Contro
>Il fatto di non adottare nessun particolare accorgimento nell’inserimento dei record che possa poi facilitare la ricerca:
>- ci fornisce le prestazioni peggiori in termini di numero di accessi in memoria richiesti dalle operazioni di ricerca 
>- mentre l’inserimento è molto veloce se ammettiamo duplicati

>[!note] Operazioni
>- [[#Ricerca]]
>- [[#Inserimento]]
>- [[#Modifica]]
>- [[#Cancellazione]]

---
## Ricerca

Se si vuole ricercare un record occorre scandire tutto il file, iniziando dal primo record fino ad incontrare il record desiderato.



---
## Inserimento 



---
## Modifica



---
## Cancellazione

