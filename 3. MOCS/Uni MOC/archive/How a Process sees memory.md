---
type: Uni Note
class:
  - "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2026-07-04T18:27
updated: 2026-07-05T11:36
---
## 1. Lo spazio di indirizzamento di un processo

Ogni processo, quando viene eseguito, ha a disposizione un proprio **spazio di indirizzamento virtuale**, organizzato in diverse regioni (segmenti). Ogni segmento ha uno scopo preciso, regole di accesso diverse (lettura/scrittura, condivisione tra processi) e un comportamento diverso a runtime.

Schema concettuale (non in scala):

```
Indirizzi alti
┌───────────────────────┐
│         Stack           │  ← cresce verso il basso
│           ↓              │
├───────────────────────┤
│                         │
│    (spazio libero)      │  ← enorme su sistemi 64 bit
│                         │
├───────────────────────┤
│           ↑              │
│         Heap             │  ← cresce verso l'alto
├───────────────────────┤
│   BSS (dati non init.)  │
├───────────────────────┤
│ Data (dati inizializzati)│
├───────────────────────┤
│         Text             │  ← codice, read-only
└───────────────────────┘
Indirizzi bassi
```

---
## 2. Text (Code segment)

- Contiene il **codice macchina eseguibile** del programma.
- È tipicamente **read-only**: un programma non deve modificare le proprie istruzioni durante l'esecuzione (protezione da bug e attacchi).
- **Può essere condiviso** tra più processi che eseguono lo stesso programma (es. più istanze di `bash`): non serve duplicarlo in RAM per ogni processo.
- Dimensione fissa, decisa a compile-time/link-time.

---

## 3. Data segment

Contiene le **variabili globali e statiche**. Si divide in due sotto-sezioni, per motivi di efficienza:

### 3.1 Initialized data
- Variabili globali/statiche con un **valore iniziale esplicito diverso da zero** nel codice sorgente.
- I valori concreti devono essere salvati fisicamente nel file eseguibile.

### 3.2 BSS (Block Started by Symbol)
- Variabili globali/statiche **non inizializzate** (o inizializzate a zero).
- Il file eseguibile **non contiene i dati veri e propri**, ma solo un numero: "quanto spazio serve, riempilo di zero al caricamento".

**Perché la distinzione BSS / initialized data?**
- **Risparmio di spazio su disco**: evita di dover salvare esplicitamente megabyte di zeri nell'eseguibile per array/buffer globali non inizializzati.
- **Caricamento più veloce**: azzerare memoria è più efficiente che copiare dati specifici da un file (il sistema può usare pagine già azzerate, allocazione lazy, copy-on-write).

| Sezione | Contenuto nel file eseguibile | Spazio su disco |
|---|---|---|
| Initialized data | Valori veri e propri | Proporzionale ai dati |
| BSS | Solo la dimensione richiesta | Quasi nullo |

- Sia data che BSS sono **read-write** e **non condivisi** tra processi diversi (ogni processo ha la propria copia privata).

---

## 4. Heap

- Memoria allocata **dinamicamente a runtime** (es. tramite `malloc` in C).
- Cresce **verso l'alto** (verso indirizzi crescenti), gestita tramite `brk()`/`sbrk()` o `mmap()`.
- Se non c'è più spazio virtuale disponibile da mappare, le allocazioni falliscono (`malloc` restituisce `NULL`).

---

## 5. Stack

- Contiene i **record di attivazione** (stack frame) delle funzioni: parametri, indirizzo di ritorno, **variabili locali**.
- Cresce e si riduce dinamicamente con le chiamate/ritorni di funzione.
- Cresce tipicamente **verso il basso** (verso indirizzi decrescenti).
- **Privato per ogni processo** (e per ogni thread, se il processo è multi-threaded).
- Ha un **limite massimo configurabile** (es. `ulimit -s`, spesso 8 MB di default): oltre quel limite, un tentativo di crescita causa un **segmentation fault** (SIGSEGV) invece di un consumo incontrollato di memoria.

---

## 6. Perché heap e stack non si "scontrano" nella pratica

- Crescono l'uno verso l'altro, ma partono così distanti (su sistemi a 64 bit, lo spazio virtuale disponibile è enorme, es. decine/centinaia di TB) che **in pratica non si toccano mai** in un uso normale.
- Lo spazio "vuoto" in mezzo è **solo virtuale**: non consuma RAM né altre risorse finché non viene effettivamente mappato/usato.
- Se una delle due regioni prova a invadere spazio non suo, il kernel intercetta l'accesso tramite un **page fault** e termina il processo (SIGSEGV) se l'accesso non è legittimo.
- Gli indirizzi esatti di partenza di stack, heap e librerie sono inoltre **randomizzati** ad ogni esecuzione tramite **ASLR** (Address Space Layout Randomization), per motivi di sicurezza (rende più difficili exploit basati su indirizzi noti).

---

## 7. Esempio pratico

```c
#include "stdlib.h"

int c = 10;
struct s {
    int sx;
    int sy;
};
struct s ses[2];
struct s ass = {1,2};

int main() {
    int x = 0;
    int *list = (int*) malloc(sizeof(int));
    return 0;
}
```

### Dove finisce ogni elemento

| Elemento | Tipo | Regione di memoria | Perché |
|---|---|---|---|
| `c` | Globale, inizializzata (≠0) | **Data (initialized)** | Valore esplicito da salvare nel file |
| `ses` | Globale, non inizializzata | **BSS** | Nessun valore esplicito: basta la dimensione |
| `ass` | Globale, inizializzata | **Data (initialized)** | Valori `{1,2}` espliciti da salvare |
| `x` | Locale a `main()` | **Stack** | Variabile automatica: sempre sullo stack, a prescindere dall'inizializzazione |
| `list` (il puntatore) | Locale a `main()` | **Stack** | È una variabile automatica come `x` |
| `*list` (l'int puntato) | Allocato con `malloc` | **Heap** | Allocazione dinamica a runtime |

### Schema visivo per questo esempio

```
Indirizzi alti
┌───────────────────────┐
│  Stack: x, list (ptr)   │
├───────────────────────┤
│    (spazio libero)      │
├───────────────────────┤
│  Heap: *list (l'int)    │
├───────────────────────┤
│  BSS: ses[2] (16 byte)  │
├───────────────────────┤
│  Data: c = 10,           │
│        ass = {1,2}      │
├───────────────────────┤
│  Text: codice di main() │
└───────────────────────┘
Indirizzi bassi
```

### Punto chiave da ricordare

La distinzione **data/BSS** vale solo per variabili **globali o `static`**. Le variabili **locali** (come `x` e il puntatore `list`), inizializzate o no, vivono sempre nello **stack** come parte del record di attivazione della funzione — non hanno nulla a che fare con la distinzione data/BSS, che riguarda esclusivamente il layout dell'eseguibile a livello di variabili globali.