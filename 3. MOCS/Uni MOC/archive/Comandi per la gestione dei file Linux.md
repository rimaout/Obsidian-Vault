---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: true
created: 2025-10-05T16:06
updated: 2025-10-05T19:11
---
## Redirezione output in bash

In bash con i simboli `>` e `<` possono essere utilizzati per redirigere l’output di un comando su di un file:

>[!note] Redirezione dell'output (>)
>
>Serve per **scrivere** l'output di un comando in un file (*sovrascrive* il contenuto del file, se esiste)
>
>```bash
>ls > elenco.txt
>```

>[!note] Redirezione con append (>>)
>
>Simile a `>`, ma **aggiunge (append)** l’output in fondo al file, senza sovrascrivere.
>
>```bash
>echo "Nuova riga" >> file.txt
>```

>[!note] Redirezione dell'input (<)
>Serve per **leggere** l'input da un file invece che dalla tastiera (standard input).
>
>```bash
>sort < nomi.txt
>```
>
>Ordina le righe contenute nel file `nomi.txt`.
Ottimo riepilogo! Ora rispondo alla tua **ultima domanda**:

| Comando                   | Effetto                                                        |
| ------------------------- | -------------------------------------------------------------- |
| `ls > file.txt`           | Scrive solo l'**output** su `file.txt`, errori sempre visibili |
| `ls 2> file.txt`          | Scrive solo gli **errori** su `file.txt`, output visibile      |
| `ls > out.txt 2> err.txt` | Scrive output in `out.txt` ed errori in `err.txt`              |
| `ls > tutto.txt 2>&1`     | Scrive sia output che errori in `tutto.txt`                    |
| `ls 2>/dev/null`          | Nasconde gli **errori**, mostra solo l'output                  |
| `ls > /dev/null`          | Nasconde l'**output**, mostra solo gli errori                  |
| `ls > /dev/null 2>&1`     | Nasconde **entrambi** (né output né errori visibili)           |

## Comandi

>[!note] unmusk
>
>Il comando `umask` in Linux viene utilizzato per impostare la "maschera di creazione dei file", ovvero la quantità di permessi da rimuovere automaticamente dai permessi di default quando si crea un nuovo file o una nuova directory.
>
>Se eseguiamo solamente `umask` otteniamo come output l'attuale maschera utilizzata:
>- `umask` -> `0022` (es.)
>- `umask -S` -> `u=rwx,g=rx,o=rx` (es.)
>
>>[!warning] Esempio con calcoli
>>
>>Immaginiamo di avere un file e una directory con permessi rispettivamente settati a `666` e `777`, se applichiamo `umask 022` otteniamo he i permessi risultanti sono:
>>- *file:* 666 - 022 = 644 -> rw-r--r--
>>- *dir:* 777 - 022 = 755 -> rwxr-xr-x
>
>Vedi anche [[Permessi File Linux]]

>[!note] cp
>
>Il comando `cp` permette di copiare uno più file in data destinazione, sintassi, timestamp, link e attributi speciali. Se utilizzato su una cartella effettuerà anche una copia ricorsiva.
>
>```bash
>cp [-r] [-i] [-u] [-a] {file sorgenti} destinazione
>```
>
>- `-r` recursive per directory
>- `-i` interactive per essere avvisati in caso di sovrascrizione
>- `-u` la sovrascrittura avviene solo se l'`mtime` del sorgente e più recente di quello della destinazione
>- `-a` (archive) preserva gli attributi dei file (non delle directory):
>	- Preserva i collegamenti simbolici (symlink)
>	- Preserva i permessi (read, write, execute)
>	- Preserva la proprietà (utente e gruppo)
>	- Preserva i timestamp (data e ora di modifica, accesso, ecc.)
>
>Modalità *archive* se utilizziamo l'opzione `-a`, preserva gli attributi come permessi, proprietari, gruppi,  
>
>Copiare più file simultaneamente: `cp file1.txt file2.txt file3.txt /percorso/destinazione/`

>[!note] mv
>
>Il comando `mv` permette di spostare (move) uno o più file da una sorgente ad una destinazione.
>
>```bash
>mv [-i] [-u] [-f] {filesorgenti} destinazione
>```
>
>- `-i` interactive per esserre avvisati in caso di sovrascrizione
>- `-u` la sovrascrittura avviene solo se l'`mtime` del sorgente e piu recente di quello della destinazione
>- `-f` non mostra messaggi interattivi, sovrascrive file esistenti senza chiedere (non unire con `-i` o `-u`)
>  
>Utilizzare `mv` per **rinominare** file e directory:
>- Rinominare un file nella stessa directory: `mv vecchio_nome.txt nuovo_nome.txt`
>- Spostare e rinominare un file in un'altra directory: `mv /percorso/vecchio.txt /altro/percorso/nuovo_nome.txt`
>- Rinominare una directory: `mv VecchiaCartella NuovaCartella`
>- Spostare e rinominare una directory in un'altra directory: `mv /percorso/VecchiaDir /altro/percorso/NuovaDir`

>[!note] rm
>
>Il comando `rm` permette di rimuovere file e, con opzioni, directory e loro contenuto.
>
>```bash
>rm [-i] [-f] [-r | -R] [-v] {file...}
>```
>
>- `-i` chiede conferma per ogni file prima di cancellarlo (interactive).
>- `-f` forza la rimozione: non mostra messaggi di errore per file inesistenti e non richiede conferme; `-f` ha priorità su `-i`.
>- `-r` o `-R` rimuove ricorsivamente directory e tutto il loro contenuto (necessario per cancellare directory non vuote).
>- `-v` verbose — mostra i file mentre vengono rimossi.
>
>Avvertenze importanti:`rm` non sposta i file nel cestino: la cancellazione è definitiva (a meno di snapshot/backup esterni).

>[!note] touch
>
>Il comando `touch` serve a modificare i timestamp di un file o directory, e se il file non esiste lo crea.
>
>```bash
>touch [-a] [-m] [-t timestamp] {file}
>```
>- `-t` serve per impostare il timestamp desiderato

>[!note] ln
>
>Il comando `ln` crea link tra file: link hard (default) che condividono lo stesso inode, o link simbolici (soft) che puntano a un percorso.
>
>```bash
>ln [-s] [-f] [-i] [-v] TARGET [LINK_NAME]
>```
>
>- `-s` crea un **link simbolico** (symlink). Senza `-s` si crea un **hard link**.
>- `-f` forza la creazione sovrascrivendo eventuali link/file esistenti con lo stesso nome.
>- `-i` chiede conferma prima di sovrascrivere (interactive).
>- `-v` verbose — mostra i link creati.
>
>Comportamenti chiave:
>- Hard link: due (o più) nomi riferiscono lo stesso inode; rimuovere un nome non cancella i dati finché esiste almeno un hard link. Non può attraversare sistemi di file diversi e non può riferirsi a directory (senza permessi speciali).
>- Symlink: file che contengono un percorso verso TARGET. Possono puntare a directory, attraversare filesystem e possono diventare "dangling" se il TARGET viene rimosso.
>
>Controllo link:
>- Visualizzare symlink con `ls -l` (mostra la freccia e il target).
>- Verificare inode (hard link) con `ls -i` o `stat filename`.
>  
>| Caratteristica                  | Hard Link                          | Symlink (Soft Link)                   |
>| ------------------------------- | ---------------------------------- | ------------------------------------- |
>| Inode condiviso                 | ✅ (stesso inode)                   | ❌ (inode diverso, contiene solo path) |
>| Attraversa filesystem           | ❌                                  | ✅                                     |
>| Può riferirsi a directory       | ❌ (solo con permessi speciali)     | ✅                                     |
>| Resta valido se TARGET sparisce | ✅                                  | ❌ (diventa "dangling")                |
>| Visibile con `ls -l`            | No differenza visibile (come file) | ✅ mostra → verso il target            |

> [!note] df
> 
> Il comando `df` (disk free) mostra lo **spazio libero e usato** nei filesystem montati. I dati sono riferiti al filesystem, **non** ai singoli file o directory.
> 
> ```bash
> df [OPZIONI] [FILE...]
> ```
> 
> - Senza argomenti, mostra l'uso del disco di **tutti i filesystem montati**.
> - Se viene fornito un file o percorso, mostra le info del filesystem che lo contiene.
>
>|Opzioni comuni|Descrizione|
>|---|---| 
>|`-h`| "Human-readable": mostra dimensioni in KB, MB, GB (es. 1G invece di 1073741824)|
>|`-i`| List inode information instead of block usage|
>|`-l`| Limit listing to local file systems (excludes remote filesystems like: `nfs`, `cifs` (Windows shares) `smb`, `sshfs`) |
>|`--total`|Aggiunge una riga finale con il totale aggregato|

> [!note] dd
> 
> Il comando `dd` copia dati **a basso livello** tra file o dispositivi, permettendo operazioni precise su blocchi. Usato per creare immagini disco, scrivere su dispositivi, backup, test di velocità, ecc.
> 
> ```bash
> dd if=INPUT of=OUTPUT [opzioni]
> ```
> 
> - `if=` (input file): sorgente dei dati (es. file, dispositivo `/dev/sdX`, ecc.)
>     
> - `of=` (output file): destinazione dei dati
> 
> |Opzioni comuni|Descrizione|
> |---|---|
> |`bs=N`|Imposta dimensione del blocco (es. `bs=1M` per 1 MiB). Sovrascrive `ibs` e `obs`|
> |`count=N`|Copia solo N blocchi|
> |`skip=N`|Salta N blocchi all’inizio dell’input|
> |`seek=N`|Salta N blocchi all’inizio dell’output (senza scriverli)|
> |`conv=...`|Converte dati (es. `notrunc`, `noerror`, `sync`, `ucase`, `lcase`, ecc.)|
> |`status=progress`|Mostra l’avanzamento in tempo reale|
> 
> |Tipo conv|Effetto|
> |---|---|
> |`notrunc`|Non tronca il file di output|
> |`noerror`|Continua in caso di errori di lettura|
> |`sync`|Riempe blocchi incompleti con zeri|
> |`fdatasync`|Forza il flush dei dati su disco prima di terminare|
 
> [!note] du
> 
> Il comando `du` (**disk usage**) mostra lo spazio occupato da file e directory, **camminando nel filesystem** e sommando i contenuti. A differenza di `df`, lavora a livello di **file/directory**, non dell’intero filesystem.
> 
> ```bash
> du [OPZIONI] [FILE...]
> ```
> 
> Se nessun file è specificato, analizza la directory corrente ricorsivamente.
> 
> |Opzioni comuni|Descrizione|
> |---|---|
> |`-h`|Mostra i valori in formato leggibile (es. KB, MB, GB)|
> |`-s`|Mostra solo il **totale** per ciascun argomento (senza dettagli ricorsivi)|
> |`-a`|Mostra anche lo spazio occupato dai **file**, non solo directory|
> |`-c`|Aggiunge una riga con il **totale complessivo**|
> |`--max-depth=N`|Limita la profondità della ricorsione (es. `--max-depth=1`)|

> [!note] mkfs
> 
> Il comando `mkfs` (**make filesystem**) serve a **formattare** un dispositivo o una partizione, creando un **nuovo filesystem** (es. ext4, xfs, fat32, ecc.). Distrugge tutti i dati esistenti.
> 
> ```bash
> mkfs -t tipo_fs [fsoptions] DISPOSITIVO
> ```
> 
> - `-t` → specifica il **tipo di filesystem** (es. `ext4`, `vfat`, `xfs`, ecc.)
> - `fsoptions` → opzioni specifiche del filesystem, come `ro` (read only) e `rw` (read & write)
> - `DISPOSITIVO` → partizione o disco su cui creare il filesystem (es. `/dev/sdb1`)
>
>>[!danger] Perdita dati
>>- **Tutti i dati verranno cancellati**. Usare solo su dischi o partizioni di cui si è certi.
>>- Verifica sempre il dispositivo prima di procedere (con `lsblk`, `fdisk -l`, `blkid`).


