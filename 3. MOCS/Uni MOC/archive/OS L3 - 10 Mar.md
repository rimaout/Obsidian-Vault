---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-03-10T17:42
updated: 2025-03-12T10:50
---
## Il filesystem root

## Mounting

## Tipi di Filesystem

## File passwd e group

Sono file che possono essere rispettivamente trovati in `/etc/passwd` e `/etc/group`, sono file di testo con codifica 8 bit, con una struttura specifica conosciuta dai programmi che interagiscono con questi file.

Sono organizzati per righe, ovvero sequenze di caratteri terminati dal carattere _line feed_ LF (0x0A); dove ogni riga contiene capi separati da `:`.

>Nell file **passwd** ogni riga rappresenta un user con questa struttura:
>
>```
>username:password:uid:gid:gecos:homedir:shell
>```
>
>>***oss:*** al posto di password ci sarà una `x`, l'hash della vera password è salvato nel file protetto `shadow`.

>Nel file **group** clxjkjskjbld


## File

Ogni file nel filesystem è rappresentato da una struttura dati inode ed è univocamente identificato da un inode number.

>[!note] Attributi di struttura dati inode
>
>- *Type:*
>- *User ID:*
>- *Group ID:*
>- *Mode:*
>- *Size:*
>- *Timestamps:*
>- *Link count:*
>- *Data pointers:*

#### Tabella inod

#### Come visualizzare le informazioni di un inode

abbiamo due comandi possibili `ls` e `stat`

**ls**
- `-i`: ritorna il numero del *inode*
- `-l`: mostra varie informazioni *diritti, user, group, date, size, time*.


>la sezione dimensione mostra lo spazzio occupato da un file dlfhsakldjfh

**stat**

## Permessi di accesso

I permessi di accesso indicano chi può fare cosa.

- ***Utente proprietario:*** solitamente chi crea il file/directory
- ***Gruppo proprietario:*** gruppo primario dell’utente proprietario (specificato in `/etc/passwd`)

 Il proprietario definisce i permessi di accesso ovvero chi può leggere, scrivere, eseguire un file/directory.

>[!note] Permessi accesso a File
>
>![[Pasted image 20250312091455.png|700]]

>[!note] Permessi di acesso a Directory
>
>![[Pasted image 20250312091057.png|800]]

## Permessi Speciali

Esistono altri tre tipi di permessi detti speciali che possono essere utilizzate sia su `file` che `directory`:
- [[#^523498|sticky bit (t)]]
- [[#^c14558|setuid bit (s)]]
- [[#^3a7226|setgid bit (s)]]

>[!note] sticky bit (t)
>
>Applicato su directory corregge il comportamento di `w+x`, obligando l'utente ad avere i permessi di scrittura sul file per cancellarlo.
>
>Infatti senza sticky bit se l'utente ha permesso `w+r` sulla directory ma non sui file della directory, può comunque cancellare i file.
>
>>***oss:*** sticky bit è inutile sui file.

^523498

>[!note] setuid bit (s)
>
>Si utilizza solo per i file eseguibili, quando vengono eseguiti, i privilegi con cui opera il corrispondente processo non sono quelli dell'utente che esegue il file, bensi quelli dell'utente proprietario del file.
>
>Quindi, se il proprietario e’ root, viene eseguito con i privilegi di root, indipendentemente da chi lo ha eseguito

^c14558

>[!note] setgid bit (s)
>
>Analogo di `setuid` ma con i gruppi. I privilegi sono quelli del gruppo del file eseguibile.
>
 Può essere applicato anche ad una directory, e allora ogni file creato li dentro ha il gruppo della directory, anziché quello primario di chi crea i files.

^3a7226

il setuid rimpiazza la x nella terna user con una s
il setgit rimpiazza la x nella terna group con una s
il sticky rimpiazza la x nella terna other con una t

## Comando chmod

https://www.freecodecamp.org/italian/news/permessi-sui-file-in-linux-come-usare-il-comando-chmod/

**chmod** è un comando che ti consente di cambiare i permessi (modalità) per un file o directory.

Con sintassi: `chmod <Operazioni> <Nome File/Directory>`

## Modalità simbolica

Una lettera tra `ugo` per indicare la terna che vogliamo modificare, dove:
- `u` india `user`
- `g` indica `group`
- `o` indica `other`

Una (o più) lettere tra `rxwst` per indicare ili permesso che vogliamo modificare, dove:
- `r` indica `read`
- `x` indica `execute`
- `w` indica `write`
- `s` indica `setuid` (se utilizzato su user) o `setgid` (se utilizzato su group)
- `t` indica `sticky`

Un operatore tra *-*, *+* o *=* dove:
- *-* indica la rimozione di un permesso
- *+* indica l’aggiunta o la sovrascrittura di un permesso
- *=* modifica i permessi di un intera tripla

