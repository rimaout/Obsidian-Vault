---
type: Uni Note
class:
  - "[[Sistemi Operativi 2 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-10-03T17:50
updated: 2025-10-07T09:58
---

I permessi di accesso indicano chi può fare cosa.

- ***Utente proprietario:*** solitamente chi crea il file/directory
- ***Gruppo proprietario:*** gruppo primario dell’utente proprietario (specificato in `/etc/passwd`)

 Il proprietario definisce i permessi di accesso ovvero chi può leggere, scrivere ed eseguire un file/directory.

>[!note] Permessi accesso a File
>
>![[Pasted image 20250312091455.png|700]]

>[!note] Permessi di acesso a Directory
>
>![[Pasted image 20250312091057.png|800]]

## Permessi Speciali

Esistono altri tre tipi di permessi detti speciali che possono essere utilizzate sia su `file` che `directory`:
- [[#^c14558|setuid bit (s)]]
- [[#^3a7226|setgid bit (s)]]
- [[#^523498|sticky bit (t)]]

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

>[!note] sticky bit (t)
>
>Applicato su directory corregge il comportamento di `w+x`, obbligando l'utente ad avere i permessi di scrittura sul file per cancellarlo.
>
>Infatti senza sticky bit se l'utente ha permesso `w+r` sulla directory ma non sui file della directory, può comunque cancellare i file.
>
>>***oss:*** sticky bit è inutile sui file.

^523498

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

