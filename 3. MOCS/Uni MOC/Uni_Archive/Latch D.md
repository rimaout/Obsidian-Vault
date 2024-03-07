---
Created: 2023-11-06
Type: Uni Note
Class:
  - "[[Progettazione Sistemi Digitali (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Circuiti sequenziali]]"
  - "[[Latch SR]]"
Completed: true
---
---
## Indice:
1. [[#Definizione]]
2. [[#Circuito + Funzionamento]]

---
## Definizione
- Il **Latch D** (latch delay) è un circuito [[Circuiti sequenziali|sequenziale]] ed [[Circuiti Sincroni ed Asincroni#Circuiti Asincroni|asincrono]] basato sul [[Latch SR]] che permette di memorizzare un bit ma eliminando lo stato indefinito del [[Latch SR]].
- Latch D è implementazione del [[Latch SR]], ottenuto sostituendo l'input `S` con `D`  e l'input `R` con il **complemento** di `D`

>[!warning] Rappresentazione circuitale
>![[Pasted image 20240205145109.png|300]]

>[!warning] I/O
>**Input:**
>- *d* = bit in input
>
>**Output:**
>- *y* = Stato del latch (output)

---
## Circuito + Funzionamento

>[!warning] Circuito
>![[Pasted image 20240205145447.png|350]]

>[!warning] Tabella stati
>![[Pasted image 20240205150401.png|200]]

---