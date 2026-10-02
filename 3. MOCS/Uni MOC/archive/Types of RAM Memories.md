---
type: Uni Note
class:
  - "[[Bachelor Thesis]]"
academic year: 2024/2025
related:
completed: true
created: 2026-10-02T08:31
updated: 2026-10-02T10:07
tags:
  - gpu
  - hpc
  - cerebras
  - RAM
aliases:
  - SRAM
  - DRAM
  - HBM
  - GDDR
  - RAM Technologies
---
> [!abstract] In sintesi
> - **SRAM** e **DRAM** sono *tecnologie* (come è fatto il bit); **DDR, GDDR e HBM** sono *famiglie di DRAM* (come i chip si collegano al processore); **VRAM** è un *ruolo* (la memoria locale della GPU, in GDDR o HBM).
> - La SRAM è veloce e sta sul die, ma è piccola e costosa. La DRAM è grande ed economica, ma è lenta e sta fuori dal die.
> - Questo divario è all'origine della **memory wall** delle GPU.

Collegamenti: [[Cerebras WSE Introduction|Cerebras WSE-3]] · [[Type of GPUs Interconnections (PCIe and NVLink)|PCIe e NVLink]]

---

## SRAM vs DRAM

### SRAM (Static RAM)

Ogni bit è memorizzato in un circuito bistabile di **6 transistor (6T)**: due inverter in anello più due transistor di accesso. Finché c'è alimentazione, il valore resta stabile.

- Molto veloce (accesso in pochi cicli) e senza refresh.
- Occupa molta area (6 transistor per bit) e costa molto per bit.
- Si realizza con lo **stesso processo dei transistor logici**, quindi può stare sullo stesso die dei core. Per questo è la tecnologia di registri, cache e shared memory.

### DRAM (Dynamic RAM)

Ogni bit è un **transistor + un condensatore (1T1C)**: il bit è la presenza o l'assenza di carica nel condensatore.

- Molto più densa (un solo transistor per bit), quindi più economica per GB.
- La carica **si disperde**: ogni riga va rinfrescata periodicamente (tipicamente ogni ~64 ms).
- La lettura è **distruttiva**: leggere una riga scarica i condensatori e bisogna riscriverla.
- Accesso più lento: si "apre" una riga intera (*row activate*) nei sense amplifier (il *row buffer*) e poi si seleziona la colonna (*column access*). Accedere a una riga già aperta è molto più veloce che aprirne una nuova.
- I condensatori richiedono un processo di fabbricazione diverso da quello logico, quindi la DRAM **si produce in chip separati**.

> [!warning] Cerebras e la SRAM
> Il [[Cerebras WSE Introduction|WSE-3]] usa SRAM per tutti i suoi 44 GB e, per farlo, dedica circa metà dell'area di ogni core alla memoria. Ottiene banda e latenza fuori scala, ma paga con una capacità molto minore di quella ottenibile con la DRAM.

---

## Le memorie dentro una GPU

| Livello | Tecnologia | Dove | Capacità (H100) | Latenza indicativa |
|---|---|---|---|---|
| Registri | SRAM | Dentro ogni SM | ~256 KB per SM | ~1 ciclo |
| L1 / Shared memory | SRAM | Dentro ogni SM | ~256 KB per SM (configurabile) | ~20-30 cicli |
| L2 cache | SRAM | Sul die, condivisa | ~50 MB | ~200 cicli |
| Global memory (VRAM) | DRAM (HBM o GDDR) | Fuori dal die | 80 GB | diverse centinaia di cicli |

Nota il salto di capacità tra L2 (decine di MB) e global memory (decine di GB): è il motivo per cui la memory wall esiste.

---

## Famiglie di DRAM: DDR, GDDR, HBM

Sono tutte DRAM: cambia **come i chip vengono collegati al processore**. La banda dipende da due parametri:

$$
\text{Banda} = \frac{\text{larghezza del bus (bit)} \times \text{velocità per pin (Gbit/s)}}{8}
$$

Si può ottenere la stessa banda con un bus **stretto e velocissimo** (GDDR) o con un bus **larghissimo e più lento** (HBM).

### DDR (es. DDR5): la RAM di sistema

- Moduli (DIMM) inseriti in slot sulla scheda madre, lontani dalla CPU.
- Ogni canale è largo 64 bit. DDR5-4800: $64 \times 4{,}8 / 8 = 38{,}4$ GB/s per canale.
- Un server con 12 canali arriva a ~460 GB/s.
- Punto di forza: **capacità** (fino a TB) ed espandibilità, non la banda.

### GDDR (es. GDDR6, GDDR6X, GDDR7): la memoria per grafica

- Chip saldati sulla scheda, vicini alla GPU, ciascuno con interfaccia a 32 bit.
- Molti chip in parallelo formano un bus da 256-512 bit, con pin molto veloci (16-32 Gbit/s).
- Esempio, RTX 4090: bus a 384 bit con GDDR6X a 21 Gbit/s → $384 \times 21 / 8 \approx 1$ TB/s.
- **Pro:** tecnologia matura, economica, facile da montare sul PCB.
- **Contro:** segnali velocissimi su tracce di rame lunghe consumano molta energia e pongono limiti di integrità del segnale. Per questo è usata in GPU consumer e di fascia media, non negli acceleratori di punta.

### HBM (High Bandwidth Memory): la memoria degli acceleratori AI

- Più die DRAM (4, 8, 12, 16) sono **impilati verticalmente** e collegati da **TSV (Through-Silicon Vias)**: fori verticali conduttivi che attraversano il silicio.
- Ogni stack ha un'interfaccia larga **1024 bit**. Gli stack sono montati accanto alla GPU su un **interposer di silicio** (packaging 2.5D, es. CoWoS di TSMC), che offre migliaia di collegamenti cortissimi tra GPU e memoria.
- Esempio, HBM3 al massimo dello standard (6,4 Gbit/s per pin): $1024 \times 6{,}4 / 8 \approx 819$ GB/s per stack.
- **H100:** 5 stack attivi → bus da 5120 bit → ~3,35 TB/s (con una velocità per pin inferiore al massimo dello standard).
- **B200:** 8 stack HBM3e → bus da 8192 bit → ~8 TB/s.
- **Pro:** banda altissima, consumo per bit più basso (collegamenti corti e lenti ma paralleli), ingombro ridotto.
- **Contro:** costo elevato, produzione difficile (impilare e collegare i die è complesso e la resa conta), calore concentrato nello stack, packaging su interposer che è oggi un collo di bottiglia produttivo. Il numero di stack è inoltre limitato dal **perimetro del die**, perché la memoria deve stare sul bordo.

---

## Riepilogo

| | SRAM | DDR | GDDR | HBM |
|---|---|---|---|---|
| **Cella** | 6T | 1T1C | 1T1C | 1T1C |
| **Posizione** | Sullo stesso die | DIMM sulla scheda madre | Chip sulla scheda, vicino alla GPU | Stack sull'interposer, accanto alla GPU |
| **Banda tipica** | Molto alta (locale) | ~40 GB/s per canale | ~0,5-1 TB/s | ~3-8 TB/s |
| **Capacità** | KB - decine di MB | Fino a TB | 8-48 GB | 80-200 GB |
| **Costo per GB** | Altissimo | Basso | Medio | Alto |
