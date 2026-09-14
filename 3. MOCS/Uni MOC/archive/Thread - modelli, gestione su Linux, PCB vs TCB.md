---
type: Uni Note
class:
  - "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2026-07-05T11:36
updated: 2026-07-05T11:38
---
## 1. Modelli di threading

### Thread a livello utente (User-Level Threads, ULT)
- Gestiti interamente da una **libreria in user space** (es. vecchie "green threads"), **senza che il kernel ne sappia nulla**
- Il kernel vede **un solo processo/task** — nessuna visibilità sui thread creati internamente
- Lo **scheduling tra thread** avviene interamente in user space, gestito dalla libreria

**Vantaggi**: creazione/switch tra thread molto veloce (nessun mode switch verso il kernel necessario)

**Svantaggio enorme**: se un thread fa una **system call bloccante** (es. `read()` che si blocca in I/O), **l'intero processo si blocca** — il kernel vede un solo task e non sa che ci sono altri thread pronti a girare. Inoltre non si può sfruttare il **multiprocessing reale** (i thread non possono girare veramente in parallelo su core diversi).

### Thread a livello kernel (Kernel-Level Threads, KLT)
- **Ogni thread è visibile al kernel come un task a sé stante**, con la propria struttura dati di controllo
- Lo **scheduler del kernel** gestisce direttamente ogni singolo thread

**Vantaggi**:
- Se un thread si blocca in una system call, gli **altri thread dello stesso processo continuano a girare**
- **Vero parallelismo**: thread diversi dello stesso processo possono girare davvero in contemporanea su core diversi

**Svantaggio**: overhead maggiore rispetto agli ULT nella creazione/gestione (anche se molto meno costoso di un `fork()` completo, perché non copia l'intero address space)

### Modello ibrido: Many-to-Many (M:N)
Una libreria user space gestisce **molti** thread utente, mappandoli su un numero **minore** di thread kernel (invece che 1:1). Esempi storici: green threads di Java, goroutine di Go.

### Confronto

| Modello | Scheduling gestito da | Il kernel vede i thread? | Un blocco ne blocca altri? | Parallelismo multi-core |
|---|---|---|---|---|
| **User-level (ULT)** | Libreria user space | No | Sì (blocca tutto il processo) | No |
| **Kernel-level (KLT)** | Scheduler del kernel | Sì | No | Sì |
| **Many-to-many (M:N)** | Ibrido | Parzialmente | Dipende | Sì, parziale |

**Linux usa il modello 1:1 (kernel-level)**: ogni thread utente (`pthread`) corrisponde esattamente a un thread kernel — nessun multiplexing intermedio.

---

## 2. Thread su Linux: `clone()`

Linux **non distingue processi e thread a livello di kernel**: entrambi sono **task**, rappresentati dalla struttura `task_struct`. La system call **`clone()`** generalizza `fork()`, con flag che decidono **cosa condividere** invece di copiare:

```c
CLONE_VM | CLONE_FS | CLONE_FILES | CLONE_SIGHAND | CLONE_THREAD | ...
```

- **`fork()`** ≈ `clone()` **senza condivisione** — copia (concettualmente) address space, file descriptor table, ecc.
- **`pthread_create()`** ≈ `clone()` **con condivisione** di address space, file descriptor, filesystem info, gestori di segnale

## 3. Cosa condividono i thread

**Condiviso** (grazie a `CLONE_VM` e affini — stessa page table):
- **Text** (codice)
- **Data** e **BSS**
- **Heap**
- File descriptor table
- Working directory, umask
- Gestori di segnale

Se un thread scrive nell'heap, tutti gli altri thread dello stesso processo lo vedono immediatamente — non c'è copia, è letteralmente lo stesso address space.

**Privato per ogni thread**:
- **Stack** — necessario: se due thread condividessero lo stesso stack, le chiamate a funzione e variabili locali si sovrapporrebbero in modo catastrofico
- **Registri della CPU**, incluso il **program counter**
- **Thread ID (TID)**
- Segnali pendenti specifici del thread
- **Thread-Local Storage (TLS)**: variabili `__thread`/`thread_local`, che sembrano globali nel codice ma hanno una copia distinta per thread

```
Address space condiviso da tutti i thread del processo:
┌─────────────────────────┐
│  Stack thread 1 (privato) │
├─────────────────────────┤
│  Stack thread 2 (privato) │
├─────────────────────────┤
│  Stack thread 3 (privato) │
├─────────────────────────┤
│      Heap (condiviso)     │
├─────────────────────────┤
│  BSS / Data (condivisi)   │
├─────────────────────────┤
│      Text (condiviso)     │
└─────────────────────────┘
```

## 4. Perché questo design

- **Semplicità nel kernel**: un solo scheduler, una sola struttura dati (`task_struct`) sia per processi che thread
- **Efficienza nella creazione**: creare un thread è molto più economico di un `fork()` completo, perché si condivide direttamente invece di copiare (o predisporre copy-on-write per) l'intero address space

---

## 5. PCB vs TCB

### Modello classico (didattico)
- **PCB (Process Control Block)**: struttura per un intero processo — address space, file aperti, PID, stato globale, priorità
- **TCB (Thread Control Block)**: struttura per un singolo thread — registri, stack privato, TID, stato del thread. Più TCB fanno riferimento a un solo PCB

```
┌─────────────── PCB ───────────────┐
│ address space, file, PID, ecc.     │
│  ┌─ TCB 1: registri, stack, TID    │
│  ├─ TCB 2: registri, stack, TID    │
│  └─ TCB 3: registri, stack, TID    │
└─────────────────────────────────┘
```

### Modello reale Linux: `task_struct`
Non esiste una TCB separata dal PCB: **ogni thread ha il proprio `task_struct` completo**, che funge sia da PCB che da TCB (contiene sia informazioni di stato/scheduling sia registri e stack privato). Più `task_struct` di uno stesso processo multi-thread **condividono puntatori** a strutture come `mm_struct` (address space) e `files_struct` (file aperti), invece di duplicarle.

```
task_struct 1 ──┐
task_struct 2 ──┼──→ stesso mm_struct (address space)
task_struct 3 ──┘──→ stesso files_struct (file aperti)

(ogni task_struct ha comunque i propri registri, PC, stack privato)
```

### Campi chiave della `task_struct` per l'identificazione

| Campo | Cosa rappresenta | Condiviso tra thread dello stesso gruppo? |
|---|---|---|
| `pid` | ID univoco del singolo task/thread (kernel) | No — unico per ciascuno |
| `tgid` (Thread Group ID) | ID del gruppo di thread (= "PID" visto da user space) | Sì — stesso per tutti |
| `group_leader` | Puntatore al `task_struct` del thread principale del gruppo | Punta allo stesso task per tutti |
| `real_parent` / `parent` | Puntatore al processo padre (relazione di creazione) | Dipende dalla gerarchia di creazione |

**Nota importante**: la funzione di libreria `getpid()` in user space restituisce il **`tgid`**, non il `pid` interno del kernel. Per questo tutti i thread di uno stesso processo "sembrano" avere lo stesso PID dall'esterno.

### Esempio concreto

```
task_struct (thread principale):
  pid = 1000
  tgid = 1000        ← è lui stesso il leader
  group_leader → se stesso
  real_parent → task_struct del processo creatore (es. bash, pid 500)

task_struct (thread 2):
  pid = 1001         ← pid kernel univoco, diverso!
  tgid = 1000        ← stesso gruppo del thread principale
  group_leader → punta al task_struct con pid 1000

task_struct (thread 3):
  pid = 1002
  tgid = 1000
  group_leader → punta al task_struct con pid 1000
```

Da `ps` o `getpid()`: tutti e tre mostrano PID **1000** (è il `tgid`). Ma in `/proc/1000/task/` si vedono le sotto-directory `1000`, `1001`, `1002` — i veri PID kernel di ciascun thread del gruppo.

### Dove risiedono PCB/TCB/`task_struct`
Sempre in **memoria kernel**, mai accessibili direttamente dallo user space — l'accesso avviene solo tramite system call gestite dal kernel.

### Riassunto

| Aspetto | PCB (modello classico) | TCB (modello classico) | Linux (`task_struct`) |
|---|---|---|---|
| Rappresenta | Un intero processo | Un singolo thread | Sia processi che thread ("task") |
| Contiene | Address space, file, PID, stato globale | Registri, stack privato, TID | Tutto insieme, con puntatori condivisi tra "gemelli" |
| Quanti per processo multi-thread | Uno | Uno per ogni thread | Uno `task_struct` per ogni thread, tutti che condividono `mm_struct`/`files_struct` |
| Dove risiede | Memoria kernel | Memoria kernel | Memoria kernel |