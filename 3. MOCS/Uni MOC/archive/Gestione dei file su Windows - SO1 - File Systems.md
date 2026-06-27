---
type: Uni Note
class:
  - "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related:
completed: false
created: 2026-06-26T17:29
updated: 2026-06-27T12:25
---
## Introduzione

A differenza di UNIX, che standardizza tutto sul concetto di Inode, Windows è basato su due File System principali:
- **FAT (File Allocation Table):** Il ***vecchio*** file system di MS-DOS. Utilizza una tabella di puntatori concatenati. È limitato ma ampiamente compatibile, motivo per cui è ancora lo standard per le chiavette USB e i dispositivi portatili.
- **NTFS (New Technology File System):** Il file system ***moderno*** di Windows. Abbandona la vecchia tabella e gestisce lo spazio tramite una **bitmap** di blocchi a dimensione fissa chiamati **Cluster**, organizzando ogni file come un insieme di attributi all'interno di un indice master.

## FAT (File Allocation Table)

Si basa su una **tabella ordinata di puntatori**. Il volume del disco viene diviso rigidamente in ***quattro regioni principali***:
1. **Boot Sector:** Contiene le informazioni per accedere al volume (tipo di FAT, puntatori) e il codice di avvio (_bootloader_) del sistema operativo.
2. **Regione FAT:** La tabella vera e propria. Mappa l'intero contenuto della regione dati. Per sicurezza e tolleranza ai guasti, ne vengono mantenute sempre *due copie identiche* nel caso una si corrompa.
3. **Root Directory:** La tabella iniziale che contiene le entry dei file della cartella radice (`/` o `C:\`).
    - _In FAT12 e FAT16:_ Ha una dimensione fissa e limitata (massimo 256 entry).
    - _In FAT32:_ È dinamica, inclusa direttamente nella regione dati senza limitazioni.
4. **Regione Dati:** Lo spazio fisico in cui risiedono i dati dei file e delle sotto-directory.

## NTFS (New Technology File System)


