---
created: 2023-10-20
type: Uni Note
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
academic year: 2023/2024
related:
  - "[[Operatori Booleani e Porte Logiche]]"
completed: true
updated: 2026-01-31T13:32
---
>[!abstract] Index
>1. [[#Introduzione]]
>2. [[#Nand]]
>3. [[#Nor]]
>4. [[#Semplificazione doppia nand o nor in cascata]]
>5. [[#Esempio]]

>[!abstract] Related
>- [[Algebra Booleana]]
>- [[Progettazione Sistemi Digitali (class)]]

---
## Introduzione

>[!tip] Tip
>Qualsiasi forma logica può essere implementata utilizzando esclusivamente porte logiche Nand o Nor
>
> - `pos` conviene utilizzare  `nor`.
> - `sop` conviene utilizzare `nand`

Facendo in questo modo si riesce a rappresentare l'espressione sop o pos in forma universale con lo stesso numero di porte logiche presenti nell'espressione originale (che utilizza le normali porte logiche)

---
## Nand

>[!note] Rappresentazione porte con Nand
>![[IMG_738E51DB26A0-1.jpeg|800]]

---
## Nor

>[!note] Rappresentazione porte con Nor
>![[IMG_D8634AD11B27-1.jpeg|800]]

---
## Semplificazione doppia nand o nor in cascata

![[IMG_E74AF58D0224-1.jpeg|600]]

---
## Esempio

![[IMG_7FA353A337B7-1.jpeg|800]]