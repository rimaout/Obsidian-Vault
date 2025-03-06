---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-03-05T09:22
updated: 2025-03-05T11:50
---
# File System

é un are a di memoria organiza in file e directory

Sia le directory che i file sono rappresentati da un struttura dati chiamata I-Node:
- Le directory sono i node contente una lista di file/directory
- Le directori formano una struttura ad albero gerarchica

Esistono file regolari che contengono:
- ASCII
- Binari

Esisono anche file non regolari: File speciali a blocchi/caratteri modellano unita’ di I/O a blocchi/caratteri.


## File sistem linux

il files sistem linux è chiamato `cont'd` ed ha una sola directory radice `/` chiamata root.

Tutti i file e directory sono contenuti direttamente o indirettamente in /

SBIN non puoi scrivere, tmp ci possono scrivere tutti

>[!warning] No duplicati
>
>Non possiamo creare file o directory con lo stesso nome, e i nomi sono case sensitice, quindi `Ciao != ciao`.


### Path

Il `path` è il percorso per raggiungere un file/directory, composto da directory separate da `\`.

>[!note] Absolute Path
L'`absulute path` è il percorso che parte dalla root per raggiungere il file/directory che vogliamo raggiungere.
>
>Può esistere il path implicito per l'utente che specifica il percorso di un file a partire dalla home directory dell'utente, ad esempio:
>
>- `/home/utente1/dir1/dir11/dir112/file.pdf` equivale `~/dir1/dir11/dir112/file.pdf` se è l'utente 1 che cerca il file.
>- Quindi il simbolo `~` (tilde) rappresenta la home directory the current user (nel esempio precedente `~` = `/home/utente1/`)

>[!note] Relative Path
>
>Path relativo è il path che inizia dalla current working directory ed arriva al file/directory che volgiamo raggiungere.
>
>Esempio:
>
>

>[!note] Comado cwd
>
>Uno altro [[comando linux]] è `cwd` (curent working directory) che ritorna la directory la directory in cui ci troviamo
>
>Il comando `cd [path]` di entrare in una directory presente nella working directory in cui ci troviamose gli passiamo un path relativo.
>
>Oppure possiamo andare in una qualsiasi directory se gli passiamo un path assoluto, in particolare `cd /` ci porta nella root directory e `cd` senza niente ci permette di andare nella home directory dello user.
>
>`cd ..` ci porta nella directoey precedente ***scrivi meglio questa cosa***
>
>`cd .` rimani nella stessa directory in cui sei, (infatti `.` è utilizzato per riferirsi alla `cwd`)

>[!note] Comando cd

>[!note] mkdir
>
>

>[!note] ls
>
>spiega che long ti fa vedere tutti i permessi di un file
	
>[!note] touch
>
>Permette di creare un file vuoto se non esiste già.
>
>In realtà il suo originale è quello di cambiare le timestamp (creato e modificato) di un file all'orario e data di quando si è runnato il comando. 

## File Nascosti

