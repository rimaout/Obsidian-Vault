---
type: Programming Note
programming language: "[[C MOC]]"
related:
  - "[[Gestione della Memoria (Introduzione)]]"
completed: false
created: 2026-06-28T12:26
updated: 2026-06-28T12:48
---
## Librerie Dinamiche (Shared Objects)

A differenza delle librerie statiche (che vengono copiate interamente dentro l'eseguibile dal linker durante la compilazione), le **librerie dinamiche** (`.so` in Linux, `.dll` in Windows) non vengono inserite nel file finale. 

Il linker inserisce nell'eseguibile (Load Module) solo un **riferimento** (un *placeholder*). Il caricamento effettivo del codice della libreria in memoria RAM viene rimandato a un momento successivo.

### Perché si usano? (Vantaggi)
* **Risparmio di Spazio (Disco e RAM):** Se 50 processi usano la libreria standard C (`libc`), sul disco non ci saranno 50 copie del suo codice. In RAM, il Sistema Operativo caricherà la libreria **una sola volta**, mappando lo spazio di memoria dei 50 processi su quell'unica area condivisa.
* **Aggiornamenti Modulari (Indolore):** Se viene scoperto un bug di sicurezza in una libreria (es. `libssl.so`), basta aggiornare quel singolo file. Tutti i programmi che la usano beneficeranno della correzione al prossimo avvio, senza dover essere ricompilati.

---

## Caricamento Dinamico a Run-time (Dynamic Loading)

Esiste un meccanismo avanzato in cui il programma non solo non include la libreria, ma non la richiede nemmeno all'avvio. È il codice stesso, durante la sua esecuzione, a chiedere esplicitamente al Sistema Operativo di caricare una determinata libreria in RAM e di estrarne una funzione.

### Esempio Pratico in C (Linux)

Il seguente codice mostra come caricare la libreria matematica ed eseguire la funzione coseno (`cos`) a tempo di esecuzione:

```c
#include <stdio.h>
#include <dlfcn.h> // Header per la gestione del Dynamic Linking (es. dlopen, dlsym)

int main() {
    // 1. Carica la libreria matematica in RAM
    void *handle = dlopen("libm.so", RTLD_LAZY);
    if (!handle) {
        fprintf(stderr, "Errore nel caricamento: %s\n", dlerror());
        return 1;
    }
    
    // 2. Estrae l'indirizzo della funzione "cos" e lo assegna a un puntatore
    double (*coseno)(double) = dlsym(handle, "cos");
    
    // 3. Esegue la funzione tramite il puntatore
    printf("Il coseno di 0 e': %f\n", coseno(0.0));
    
    // 4. Scarica la libreria dalla memoria
    dlclose(handle);
    return 0;
}
```

## Analisi Dettagliata della Riga Critica

```c 
double (*coseno)(double) = dlsym(handle, "cos");
```

Questa riga dice al programma: _"Trova l'indirizzo di memoria della funzione `cos` dentro la libreria e salvalo in una variabile speciale (un puntatore a funzione) chiamata `coseno`, definendone la firma in modo che il compilatore sappia come gestirla"_.

Si divide logicamente in due parti:

>[!note] 1. La Parte Destra (L'Azione): `dlsym(...)`
>
>La funzione `dlsym` (Dynamic Linker Symbol) interroga il loader del Sistema Operativo:
>- **`handle`**: Specifica _dove_ cercare (il riferimento alla libreria `libm.so` aperta prima).
>- **`"cos"`**: La stringa con il nome esatto della funzione da cercare nella tabella dei simboli.
>- **Ritorno**: Restituisce un indirizzo di memoria generico (`void *`), che rappresenta il punto di inizio del codice macchina di quella funzione in RAM.

>[!note] 2. La Parte Sinistra (La Dichiarazione): `double (*coseno)(double)`
>
>Poiché il C è un linguaggio fortemente tipizzato, non è possibile invocare un indirizzo di memoria generico (`void *`) senza specificare che tipo di dati accetta e restituisce. Per farlo si usa la sintassi del **Puntatore a Funzione**:
>
>| **Elemento**            | **Significato**                                                                                                                                                                          |
>| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
>| `(*coseno)`             | Dichiara che la variabile `coseno` è un **puntatore**. Le parentesi tonde sono _obbligatorie_ per evitare che il compilatore lo scambi per il valore di ritorno di una funzione normale. |
>| `(double)` _(a destra)_ | Indica i **parametri di input**. La funzione puntata si aspetta esattamente un argomento di tipo `double`.                                                                               |
>| `double` _(a sinistra)_ | Indica il **tipo di ritorno**. Specifica che la funzione, una volta eseguita, restituirà un valore di tipo `double`.                                                                     |

> [!important] Conclusione
> 
> Una volta completata questa riga, la variabile `coseno` contiene l'indirizzo fisico della funzione. Scrivere `coseno(0.0)` dice alla CPU di saltare a quell'indirizzo di memoria, passare il parametro nel registro corretto ed eseguire le istruzioni della libreria condivisa.

## Svantaggi delle Librerie Dinamiche

Nonostante l'enorme risparmio di spazio (RAM e Disco) e la facilità di aggiornamento, l'uso delle librerie dinamiche introduce delle criticità strutturali. Questi difetti spiegano perché le librerie statiche siano ancora ampiamente utilizzate.

* **Il problema delle Dipendenze ("DLL Hell"):** L'eseguibile non è autonomo. Se sul sistema ospite manca anche solo un file `.so` o `.dll` richiesto, il programma non si avvia (es. `error while loading shared libraries`). La distribuzione del software diventa più complessa, richiedendo l'uso di *package manager* o *installer* che scarichino anche le dipendenze.
* **Rottura della Compatibilità (Versioning):** Se una libreria condivisa viene aggiornata dal sistema e le sue funzioni cambiano comportamento (o vengono rimosse), tutti i programmi compilati con la versione precedente smetteranno di funzionare o crasheranno.
* **Overhead Prestazionale:**
  * *Avvio:* Il *Loader* del Sistema Operativo perde tempo a cercare il file su disco, caricarlo in memoria e mappare gli indirizzi prima di far partire il processo.
  * *Esecuzione:* Chiamare una funzione dinamica è leggermente più lento rispetto a una statica a causa dell'indirezione (il processore deve fare dei "salti" in tabelle speciali della memoria per trovare il codice effettivo).
* **Vulnerabilità di Sicurezza:** Il caricamento a *run-time* apre la porta a tecniche di iniezione di codice. Un attaccante può ingannare il SO per fargli caricare una libreria malevola al posto di quella legittima (es. *DLL Hijacking* su Windows o abuso di `LD_PRELOAD` su Linux).

## Quando usare cosa? (Statica vs Dinamica)

La scelta tra linking statico e dinamico rappresenta il classico compromesso informatico tra **spazio** e **portabilità/prestazioni**.

| Caratteristica | Libreria Dinamica (`.so`, `.dll`) | Libreria Statica (`.a`, `.lib`) |
| :--- | :--- | :--- |
| **Distribuzione** | Complessa (servono le dipendenze sul SO ospite) | **Semplice** (file *standalone*, copi e avvii) |
| **Spazio (Disco/RAM)** | **Ottimale** (il codice è condiviso tra più processi) | Pesante (codice duplicato dentro ogni eseguibile) |
| **Velocità (Performance)** | Lieve *overhead* (tempi di avvio e salti indiretti) | **Massima** (tutto il codice è già integrato e pronto) |
| **Patch di Sicurezza** | **Semplice** (aggiorni la libreria e tutti ne beneficiano) | Complessa (devi ricompilare e ridistribuire l'intero programma) |

> [!note] L'approccio moderno
> Con l'abbassamento dei costi della memoria, linguaggi di programmazione moderni (come **Go** o **Rust**) tendono a preferire il linking **statico** di default. Il principio è: *meglio avere un eseguibile più pesante di qualche megabyte, ma avere la certezza assoluta che funzionerà ovunque senza causare problemi di dipendenze all'utente.*