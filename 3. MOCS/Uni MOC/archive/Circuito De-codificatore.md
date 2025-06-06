---
created: 2023-10-29
type: Uni Note
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
academic year: 2023/2024
related:
  - "[[Circuiti combinatori]]"
  - "[[Circuito Codificatore]]"
completed: true
updated: 2024-11-18T20:21
---
>[!abstract] Index
>1. [[#Introduzione]]
>2. [[#Circuito]]

>[!abstract] Related
>- [[Circuiti combinatori]]
>- [[Circuito Codificatore]]
>- [[Progettazione Sistemi Digitali (class)]]

---
## Introduzione

È utilizzato per decodificare gli output di un [[Circuito Codificatore]]

>[!note] Rappresentazione circuitale
>![[Pasted image 20240131163252.png|150]]

>[!danger] Caratteristiche
>- È un [[Circuiti combinatori|circuito combinatorio]]
>- La funzione del Circuito De-Codificatore è opposta alla funzione del [[Circuito Codificatore]]

>[!danger] Funzionamento
>- Le linee in uscita saranno tutte 0 tranne quella nella posizione espressa (in binario) dalle linee di inpu

> **OSS:**  De-codificatore = *Array porte AND*

---
## Circuito

>[!note] Tabella verità --> Circuito
>Per ricavare il circuito da una tabella di verità in questo caso dobbiamo: 
>- Cercare le variabili che rendono l'output `1` 

>**OSS:** Il circuito di un de-codificatore è composto da sole porte `AND`.

>[!warning] Decoder 2-4
>![[IMG_2598.jpeg|600]]

>[!warning] Decoder 3-8
>![[IMG_2599.jpeg|600]]

---
