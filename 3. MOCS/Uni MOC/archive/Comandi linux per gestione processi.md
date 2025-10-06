---
type: Uni Note
class:
  - "[[Sistemi Operativi 2 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-10-05T19:31
updated: 2025-10-06T20:52
---
## Esecuzione in background  di un comando (&)

In Bash, il simbolo `&` messo *alla fine di un comando* serve per eseguire il comando in background. Questo permette di *continuare a usare il terminale* mentre il comando è ancora in esecuzione.

Ad esempio possiamo eseguire in background il comando `sleep` in questo modo:

```bash
sleep 10 &
```

Output:
- Subito viene scritto: `[1] 22035`
- Dopo 10 secondi: `[1]  + 22035 done       sleep 10`

|Parte|Significato|
|---|---|
|`[1]`|Sempre il **job number**|
|`+`|Indica che è l’**ultimo job gestito** (job "corrente")|
|`22035`|Il **PID** del processo|
|`done`|Stato finale: il processo è **terminato con successo**|
|`sleep 10`|Il comando eseguito|

## Pipe

Il simbolo `|` (**pipe**) serve per **reindirizzare l’output** di un comando verso l’**input** di un altro.

In pratica:

```bash
comando1 | comando2
```

- L’**output standard** (`stdout`) di `comando1` diventa l’**input standard** (`stdin`) di `comando2`.

Viene creato un solo job dove i comandi sono eseguiti **contemporaneamente** (in parallelo), e la pipe gestisce il flusso di dati tra di loro.

## Comandi

>[!note] jobs
>
>Il comando `jobs` elenca i job attivi nella shell corrente.
>
>```bash
>jobs [-l] [-p]
>```
>- senza niente: mostra il *job number*, lo *stato* e il *comando* dei processi
>- `-l`: aggiunge anche *PID*
>- `-p`: mostra soltanto i *PID*
>- `-e` permette di vedere i processi in esecuzione in tutti il sistema (non soltanto shell attuale)
>
>```bash
>sleep 60 &    # Avvia in background
>
>jobs
>[1]+  Running                 sleep 60 &
>
>jobs -l
>[1]+  12345 Running           sleep 60 &
>
>jobs -p
>12345
>```

> [!note] bg e fg 
> - `fg` porta un processo in **foreground** (bloccando il terminale finché non termina).
> - `bg` riprende un processo sospeso e lo manda in **background**.
>
> |Comando|Descrizione|
> |---|---|
> |`fg`|Porta in foreground il *job corrente* (`+`)|
> |`fg %n`|Porta in foreground il job con ID `n`|
> |`bg`|Riprende in background il *job corrente*|
> |`bg %n`|Riprende in background il job con ID `n`|
>
>I job possono essere identificati anche con:
>- `%prefix`: parte iniziale del comando del job (es. `%slee` per `sleep`)
>- `%%` oppure `%+`: l’*ultimo job usato* (corrente) 
>- `%-`: il *penultimo job usato*
>
>>[!example]- Esempi
>> 
>> ```bash
>> sleep 100
>> ⌨️ Ctrl + Z
>> [1]+  Stopped                 sleep 100
>> 
>> bg
>> [1]+ sleep 100 &
>> 
>> jobs
>> [1]+  Running                 sleep 100 &
>> 
>> fg
>> sleep 100   # Torna in foreground
>> ```
>
>> [!warning] bg funziona solo con job sospesi
>> 
>> Se provi a usare `bg` su un job già in esecuzione, non succede nulla, `fg` invece può riportare in primo piano sia job sospesi che attivi in background.

^baf742

> [!note] ps
> 
> Il comando `ps` mostra informazioni sui processi attivi. Di default, `ps` mostra solo i processi **associati al terminale corrente**. Per vedere più processi, servono opzioni aggiuntive.
> 
> ```bash
> ps [-e] [-u] [p]
> ```
> 
> |Comando|Descrizione|
> |---|---|
> |`ps -e`| Tutti i processi in esecuzione su tutte le shell o avviati a boot (figli del processo 0)
> |`ps -u utente`|Mostra i processi di un determinato utente|
> |`ps -p PID`|Mostra informazioni sul processo con PID|
> |`ps -o {field, ...}`| per scegliere i campi da visualizzare|
> 
>Significarono campi in output:
>- `S`: stato del processo (`R`, `S`, `Z`, `T`, `t`, `D`)
>- `UID`: ID dell'utente che ha lanciato il processo (se presente SetUID potrebbe non essere chi ha eseguito il comando)
>- `PID`: ID del processo
>- `PPID`: pid del processo che a creato questo processo (parent pid)
>- `C`: percentile di utilizzo della CPU (parte intera) 
>- `STIME`: orario di avvio del processo
>- `PRI`: attuale priorità del processo (più è alto più la priorità è bassa) 
>- `NI`: valore nice (da aggiungere alla priorità)
>- `ADDR`: indirizzo di memoria del processo (sempre vuoto, non mostrato più)
>- `SZ`: dimensione attuale del processo in numero di pagine
>- `WCHAN`: se il processo è in attesa di un qualche segnale o in sleep, qui c'è la funzione del kernel all' interno del quale si è fermato.
>- `TTY`: terminale associato
>- `TIME`: tempo CPU usato finora
>- `CMD`: comando avviato
>- `F`: è una flag associata al processo:
>	- 1 il processo è stato forkato, ma ancora non eseguito
>	- 4 ha usato privilegi da super utente
>	- 5: entrambe 1 e 4 (5 = 1 + 4)
>	- 0: nessuno dei precedenti

>[!note] top
>
>`top` è un comando interattivo che mostra in tempo reale l’elenco dei processi in esecuzione, l’uso di CPU, RAM, uptime, e molto altro
>
>Può essere visto come un `ps` ma interattivo e in tempo reale.
>
>```bash
>top [-b] [-n num] [-p {pid, ...}]
>```
>- `-b`: non accetta più comandi intentavi , ma continua a fare refresh delle informazioni
>- `-n num` fa solo `num` refresh
>- `-p {pid, ...}` mostra informazioni dei processi con pid nella lista `{pid, ...}`

>[!note] kill
>
>Il comando `kill` **non uccide sempre**: invia un segnale (di default `SIGTERM`) a uno o più processi. A seconda del segnale, può:
>- terminare
>- sospendere
>- riavviare
>- lasciare intatto un processo
>
>| Comando | Descrizione |
>|----------------------|-----------------------------------------------|  
>| `kill -l` | Elenca tutti i segnali disponibili |
>| `kill PID` | Invia `SIGTERM` al processo con PID indicato |  
>| `kill -signal PID` | Invia il segnale specificato attraverso l’identificatori `signal` al processo| 
>
>Un può essere identificato in 3 modi:
>- attraverso il suo nome (es: `STOP`)
>- attraverso `SIG` + il suono nome (es: `SIGSTOP`)
>- attraverso il suo identificatore numerico (es: per `STOP` è `19`)
>  
>Alcuni segnali utili sono (per lista completa utilizzare `kill -l`):
>- `SIGSTOP` (19) che sospendo il processo (utilizzato da `CTRL+z`)
>-  `SIGINT`(2) e `SIGKILL` (9) che interrompono il processo (utilizzato da `CTRL+c`)
>- `SIGCONT` per la continuazione dei processi sospesi (utilizzato dal comando `bg`)
>
>È possibile utilizzare la notazione con `%` (usata anche in [[#^baf742|bg e fg]]) per gestire direttamente i processi in esecuzione sulla shell.
>
>>[!warning] SIGUSR1 e SIGUSR2
>>
>>I segnali `SIGUSR1` e `SIGUSR2` sono impostati per essere usati dall'utente per le proprie necessità.
>>
>>Essi consentono una semplice forma di comunicazione tra processi
>>
>>***Esempio:*** un programma `P1` può definire un gestore del segnale (signal handler) per `SIGUSR1`. Se un programma `P2` invia un `SIGUSR1` a `P1`, allora `P1` eseguirà il codice del gestore del segnale.

^ff47ab

> [!note] nice & renice
> 
> I comandi `nice` e `renice` controllano la *priorità relativa* dei processi, influenzando quanto tempo CPU ricevono rispetto agli altri.
> 
> >***nota:*** Più alto è il valore di niceness, meno priorità ha il processo (è più "gentile" con gli altri processi).
> 
> ```bash
> nice [-n num] [comando]
> renice num {pid, ...}
> ```
> 
> |Comando|Descrizione|
> |---|---|
> |`nice comando`|Avvia un comando con priorità **di default** (`10`)|
> |`nice -n num comando`|Avvia con niceness `N` (range: `-20` = alta priorità, `19` = bassa)|
> |`renice num PID`|Cambia la niceness di un processo già attivo|
> |`renice num -u utente`|Cambia la niceness a **tutti** i processi di un utente|
> 
> >⚠️ Solo `root` può impostare un valore più basso di quello attuale (cioè aumentare la priorità).

>[!note] strace
>
>`strace` traccia le **chiamate di sistema** (come `read()`, `write()`, `open()`, `execve()`, ecc.) fatte da un processo.  
>
>È molto utile per:
>- debug di programmi che non funzionano,
>- capire cosa fa un binario,
>- trovare file mancanti, permessi negati, ecc.
>  
>|Comando|Descrizione|
>|---|---|
>|`strace comando`|Esegue il comando tracciandone le syscall|
>|`strace -p PID`|Attacca `strace` a un processo già in esecuzione|
>|`strace -o file.log comando`|Salva l'output in un file invece che a schermo|
