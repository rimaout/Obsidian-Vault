---
created: 2024-03-15
type: Uni Note
class:
  - "[[Architettura dei calcolatori (class)]]"
academic year: 2023/2024
related: []
completed: false
updated: 2024-05-27T13:29
---
---

>[!info] Index
>1. 

---
## Estensione di un numero:
- Se è un numero senza segno allora estendo aggiungendo zeri (al bit più significativo)
- Se è un numero con segno:
	- aggiungo 1 se il numero è negativo 
	- aggiungo 0 se il numero è positivo

---
## Tipi in assembly
In assembli non e esistono data types ma con numeri di byte diversi si possono rappresentare strutture dati diverse, vedremo:
- Vettori
- Matrici
- ...

## Vettori 
I assembli esistono diversi tipi di vettori che differiscono dalla grandezza dei dati al suo interno

**Vettore di byte:** 

**Vettore di caratteri (byte):** 
- per sapere quando finisce inseriamo il carattere \\0 alla fine della sequenza (in carattere \\0 è codificato dal codice Ox0)
- oss: per passare da carattere a numero fare -48

**Vettore di word:** 
- Numeri a 32 bit in complemento a due codificati in 4 byte
- Il processore mips permette l'ordinamento dei byte di una word in due modi:
	- *Big-endian:* i byte della word sono memorizzati dal most significant Byte al least significant Byte
	- *Little-endian:* i byte della word sono memorizzati dal least significant Byte al most significant Byte
---
### Accesso elementi per indice

Indirizzo dell'elemento  = indirizzo base del vettore + i x dimensione elemento

---
## Cicli (scansione di un vettore)

**Scansione per indice:**

**Scansione per puntatore:**

---
## Matrici 
una matrice $M \cdot M$ è una successione di M vettori, ciascuno di n elementi
- il numero di elementi totali è: $M\cdot N$
- la dimensione in numero di byte è: $M\cdot N\cdot \text{dimensione-elemento}$
- la si definisce staticamente come un vettore contenente $M\cdot N$ elementi uguali 

**Matrice 3d:** 2 righe, 3 colonne, 2 stati 