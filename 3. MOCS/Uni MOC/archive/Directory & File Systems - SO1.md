---
type: Uni Note
class:
  - "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2026-06-25T15:32
updated: 2026-06-25T19:52
---
## Introduzione

Le directory non sono altro che dei file speciali, che contengono altri file memorizzati sotto forma di metadati.

>[!note] Metadati dei File
>
>**Informazioni di Base:**
>- *Nome del file*  - nome scelto dal creatore, unico in una directory 
>- *Tipo del file* -  eseguibile, testo, binario, ... 
>- *Organizzazione del file* -  per sistemi che supportano diverse possibili organizzazioni
>
>**Informazioni sull’Indirizzo:**
>- *Volume* - indica il dispositivo su cui il file è memorizzato
>- *Indirizzo di partenza* 
>- *Dimensione attuale* - in byte, word o blocchi
>- *Dimensione allocata* - dimensione massima del file
>
>**Controllo di Accesso:**
>- *Proprietario* - può concedere/negare i permessi ad altri utenti
>- *Informazioni sull’accesso* - potrebbe contenere username e password per ogni utente autorizzato
>- *Azioni permesse* - per controllare lettura, scrittura, esecuzione, spedizione tramite rete
>  
>**Informazioni sull’Uso:**
>- Data di creazione 
>- Data dell’ultimo accesso in lettura
>- Data dell’ultimo accesso in scrittura 
>- Identità del creatore
>- Identità dell’ultimo lettore 
>- Identità dell’ultimo scrittore
>- Data dell’ultimo backup
>- Uso attuale: lock, azione corrente, ...
## Struttura delle Directory

La struttura e il metodo con cui vengono salvate e organizzate i file e tutte i loro metadati, è variato molto nel tempo.

>[!note] Metodo più Semplice
>
>Il metodo più semplice, utilizzato in passato, consiste nell'utilizzare **una sola directory** contenete tutti i file sul dispositivo.
>
 Ma ovviamente questo approccio porta a diversi problemi, ad esempio non si può dare lo stesso nome a due file, e con il crescere del loro numero diventa difficile mantenere l’organizzazione.

>[!note] Metodo a Due Livelli
>
>Un metodo, leggermente più avanzato, utilizzato successivamente consiste nel creare una directory per ogni utente che contiene una lista dei file di quell’utente. 
>
>Inoltre tutte le directory degli utenti sono contenute in una directory **master**.

>[!note] Schema Gerarchico ad Albero
>La struttura utilizzata ancora oggi è uno **schema gerarchico ad albero per le directory**.
>
>Qui una directory **master** contiene le directory utente che a loro volta possono contenere sia file che altre directory. Esistono anche sottodirectory di sistema.
>
>![[Pasted image 20260625195048.png|500]]
>
>La struttura ad albero permette agli utenti di trovare un file seguendo un percorso nell’albero (directory path). Nomi duplicati sono possibili purché con path diversi.


