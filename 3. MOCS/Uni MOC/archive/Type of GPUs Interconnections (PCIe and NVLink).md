---
type: Uni Note
class:
  - "[[Bachelor Thesis]]"
academic year: 2024/2025
related:
completed: true
created: 2026-10-02T08:35
updated: 2026-10-02T10:09
tags:
  - gpu
  - hpc
aliases:
  - PCIe
  - NVLink
  - NVSwitch
  - InfiniBand
  - GPU Interconnections
---
> [!abstract] In sintesi
> - **PCIe**: standard aperto per collegare CPU, GPU e periferiche. ~64 GB/s per direzione (Gen5 x16).
> - **NVLink**: link proprietario NVIDIA tra GPU, 0,9-1,8 TB/s bidirezionali per GPU, con semantica load/store.
> - **Tra nodi**: InfiniBand o Ethernet con RDMA, ~50 GB/s per porta da 400 Gb/s.
> - A ogni salto la banda cala e la latenza cresce: è il costo di scalare con più GPU invece di ingrandire il die (vedi [[Cerebras WSE Introduction#Scaling beyond the Reticle Limit|Scaling beyond the Reticle Limit]]).

Collegamenti: [[3. MOCS/Uni MOC/archive/# RDMA (Remote Direct Memory Access)]] · [[Types of RAM Memories]] · [[Reticle Limit]] · [[Cerebras WSE Introduction|Cerebras WSE-3]]

---

## PCIe (Peripheral Component Interconnect Express)

Standard generale per collegare periferiche alla CPU: GPU, schede di rete, SSD NVMe.

- **Collegamento seriale punto-a-punto.** Ogni **lane** è composta da due coppie differenziali, una per direzione, quindi è **full duplex**. I link si formano aggregando 1, 4, 8 o 16 lane (x1, x4, x8, x16). Una GPU usa tipicamente x16.
- **Velocità per generazione.** Ogni generazione raddoppia la velocità:

| Generazione | Velocità per lane | Banda x16 (per direzione) |
|---|---|---|
| Gen3 | 8 GT/s | ~16 GB/s |
| Gen4 | 16 GT/s | ~32 GB/s |
| Gen5 | 32 GT/s | ~64 GB/s |
| Gen6 | 64 GT/s | ~128 GB/s |

> [!note] GT/s
> GT/s sono *giga-transfer* al secondo (simboli sul filo, non bit utili). Da Gen3 la codifica è 128b/130b, quindi l'overhead è ~1,5%: per Gen5 x16, $32 \times 16 \times \tfrac{128}{130} / 8 \approx 63$ GB/s.

- **Topologia ad albero.** Alla radice c'è il *root complex*, integrato nella CPU. I dispositivi sono collegati direttamente o tramite *PCIe switch*. Il traffico tra due GPU dietro lo stesso switch (*GPUDirect P2P*) resta sotto lo switch; altrimenti passa dal root complex, condividendo la banda con altri dispositivi.
- **Meccanismi.** Il trasferimento avviene tramite DMA, con le periferiche mappate nello spazio di indirizzamento (*memory-mapped I/O*). In un sistema x86, un `cudaMemcpy` tra host e device viaggia su PCIe.
- **Limiti.** Banda bassa rispetto alla HBM (64 GB/s contro ~3.000 GB/s), latenza dell'ordine del microsecondo, e non è nativamente *cache-coherent*. Per questo esiste **CXL**, che costruisce la coerenza sopra il livello fisico PCIe.

---

## NVLink

Interconnessione **proprietaria NVIDIA** progettata per collegare GPU tra loro (e, nei sistemi Grace, CPU e GPU) con una banda molto più alta di PCIe.

- **Struttura.** Ogni GPU ha più link NVLink, ognuno composto da più lane differenziali ad alta velocità.
- **Banda.** NVLink 4 (H100): 18 link, **900 GB/s** totali per GPU. NVLink 5 (B200): **1,8 TB/s** per GPU. Sono valori **bidirezionali aggregati**.
- **Semantica di memoria.** Una GPU può leggere e scrivere direttamente nella memoria di un'altra con normali load/store, con atomiche e spazio di indirizzamento unificato. Non è solo copia di dati: è accesso a memoria remota.
- **NVSwitch.** Chip di switching che collega tutte le GPU in modo non bloccante (all-to-all). In un nodo HGX, 8 GPU comunicano tra loro con la banda piena. L'*NVLink Switch System* estende il dominio oltre un nodo: nei rack GB200 NVL72, 72 GPU Blackwell stanno in un unico dominio NVLink.
- **NVLink-C2C.** Variante per collegare CPU e GPU nello stesso package (Grace-Hopper), con 900 GB/s.

> [!warning] Confronto corretto con PCIe
> NVLink 4 è 900 GB/s *bidirezionali*; PCIe Gen5 x16 è ~64 GB/s *per direzione*, cioè ~128 GB/s bidirezionali. Il rapporto reale è quindi circa **7×**, non 14×.

---

## Oltre il nodo: InfiniBand ed Ethernet

Per collegare nodi diversi si usano reti come InfiniBand o Ethernet, tipicamente con porte da 400 Gbit/s (~50 GB/s per direzione). **[[3. MOCS/Uni MOC/archive/# RDMA (Remote Direct Memory Access)]]** e **GPUDirect RDMA** la scheda di rete legge e scrive direttamente nella memoria della GPU, senza passare dalla CPU. La banda resta però più di un ordine di grandezza sotto NVLink.

---

## Confronto

| | PCIe Gen5 x16 | NVLink 4 (H100) | NVLink 5 (B200) | Rete (400 Gb/s) |
|---|---|---|---|---|
| **Per direzione** | ~64 GB/s | ~450 GB/s | ~900 GB/s | ~50 GB/s |
| **Bidirezionale** | ~128 GB/s | 900 GB/s | 1,8 TB/s | ~100 GB/s |
| **Scopo** | CPU ↔ GPU, periferiche | GPU ↔ GPU | GPU ↔ GPU | Nodo ↔ nodo |
| **Semantica** | DMA, memory-mapped I/O | Load/store, atomiche | Load/store, atomiche | RDMA |
| **Standard** | Aperto (PCI-SIG) | Proprietario NVIDIA | Proprietario NVIDIA | Aperto / InfiniBand |

---

## La gerarchia di banda

| Livello | Banda (ordine di grandezza) |
|---|---|
| Shared memory / registri (aggregati sulla GPU) | decine di TB/s |
| L2 cache | alcuni TB/s |
| Link die-to-die (B200) | ~10 TB/s |
| HBM | 3-8 TB/s |
| NVLink | 0,9-1,8 TB/s |
| PCIe Gen5 x16 | ~0,06-0,13 TB/s |
| Rete tra nodi | ~0,05 TB/s |

Ogni volta che i dati escono da un livello, la banda cala e la latenza cresce. Per questo scalare oltre il reticle limit con più GPU è costoso: vedi [[Cerebras WSE Introduction#Scaling beyond the Reticle Limit|Scaling beyond the Reticle Limit]].