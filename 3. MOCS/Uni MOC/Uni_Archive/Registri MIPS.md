---
Created: 2024-03-16
Type: Uni Note
Class:
  - "[[Architettura (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Architettura MIPS]]"
  - "[[Strutta base MIPS]]"
Completed: true
---
- I 32 Registri, indicizzati da 0 a 31, della CPU principale:
	- Registro `$zero` (`$0`), contenente un valore costante pari a 0 ed immutabile
	- Registro `$at` (`$1`), usato dalle pseudo-istruzioni e dall’assemblatore
	- Registri `$v0` e `$v1` (`$2`, `$3`), utilizzati per gli output delle funzioni utilizzate nel programma
	- Registri dal `$a0` al `$a3` (`$4`, ...,`$7`) utilizzati per gli input delle funzioni
	- Registri dal `$t0` al `$t7` (`$8`, ..., `$15`), utilizzati per valori temporanei
	- Registri dal `$s0`al `$s7` (`$16`, ..., `$23`), utilizzati per valori più ricorrenti
	- Registri dal `$t8` al `$t9` (`$24`, `$25`), utilizzati per valori temporanei
	- Registri `$k0` e `$k1` (`$26`, `$27`), utilizzati dal Kernel del Sistema Operativo
	- Registro `$gp` (`$28`), ossia Global Pointer, utilizzato per la gestione della memoria dinamica
	- Registro `$sp` (`$29`), ossia Stack Pointer, utilizzato per la gestione dello Stack delle funzioni
	- Registro `$fp` (`$30`), ossia Frame Pointer, utilizzato dalle funzioni di sistema
	- Registro `$ra` (`$31`), ossia Return Address, utilizzato come puntatore di ritorno dalle funzioni
