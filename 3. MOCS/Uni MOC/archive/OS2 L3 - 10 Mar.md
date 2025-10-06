---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2025-03-10T17:42
updated: 2025-10-06T15:49
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
