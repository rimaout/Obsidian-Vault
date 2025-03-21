---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-03-12T10:42
updated: 2025-03-12T11:57
---
## Comandi per gestione file sistem


>[!note] unmusk
>
>Il comando `umask` in Linux viene utilizzato per impostare la "maschera di creazione dei file", ovvero la quantità di permessi da rimuovere automaticamente dai permessi di default quando si crea un nuovo file o una nuova directory.
>
>Se eseguiamo solamente `umask` otteniamo come output l'attuale maschera utilizzata.

>[!note] cp
>
>Il comando `cp` permette di copiare uno più file in data destinazione, sintassi, timestamp, link e attributi speciali. Se utilizzato su una cartella effettuerà anche una copia ricorsiva.
>
>```bash
>cp [-r] [-i]  [-a] [-u] {file sorgenti} destinazione
>```
>
>- `-r` recursive per directory
>- `-i` interactive per esserre avvisati in caso di sovrascrizione
>- `-u` la sovrascrittura avviene solo se l'`mtime` del sorgente e piu recente di quello della destinazione
>
>Modalità *archive* se utilizziamo l'opzione `-a`, preserva gli attributi come permessi, proprietari, gruppi,  
>
>Copiare più file simultaneamente: `cp file1.txt file2.txt file3.txt /percorso/destinazione/`

>[!note] mv

>[!note] rm

>[!note] ln

>[!note] du

>[!note] df

>[!note] dd
>