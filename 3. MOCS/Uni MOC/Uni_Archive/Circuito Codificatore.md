---
created: 2023-10-29
updated: 2024-06-12T16:41
type: Uni Note
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
academic year: 2023/2024
related:
  - "[[Circuiti Combinatori]]"
  - "[[Circuito De-codificatore]]"
completed: true
---
>[!abstract] Index
>1. [[#Introduzione]]
>2. [[#Codificatore standard e non standard]]
>3. [[#Circuito]]

>[!abstract] Related
>- [[Circuiti Combinatori]]
>- [[Circuito De-codificatore]]
>- [[Progettazione Sistemi Digitali (class)]]

## Introduzione

>[!note] Definizione
>È un [[Circuiti combinatori|circuito combinatorio]] utilizzato principalmente per ridurre il numero di linee di dati

>[!note] Rappresentazione Circuitale
>![[Pasted image 20240131163117.png|150]]

>[!danger] Caratteristiche
>- È un circuito [[Circuiti combinatori|circuito combinatorio]]
>- $2^n$ (o meno)[](Circuiti%20Combinatori.md)ircuito Codificatore]] è l'opposta al [[Circuito De-codificatore]]

>[!danger] Funzionamento 
> Le linee in uscita danno la posizione (espressa in binario) dell'unica variabile in input con valore 1.
> 
*oss:* Si assume che in qualsiasi condizione, ci sia soltanto un ingresso che valga 1.

>**OSS:** Codificatore = *Array porte OR*

---
## Codificatore standard e non standard

>[!warning] Codificatore standard
>- Utilizza il massimo numero di input rappresentabili dall'output e i numeri binari delle uscite corrispondono al pedice dell'entrata che vale 1
>
>**Esempio:** 3 output, input 8 

>[!warning] Codificatore non standard
>- Non utilizza il massimo numero di input rappresentabili dall'output o i numeri binari delle uscite non corrispondono al pedice dell'entrata che vale 1
>
>**Esempio:** 3 output , 5 input

>**oss:** 3 output --> max 8 input ($2^3$)

---
## Circuito

>[!note] Tabella verità --> Circuito
>
> Per ricavare il circuito da una tabella di verità in questo caso dobbiamo: 
> - Cercare gli input che sommati tra loro, ritornano l'output.

>**OSS:** Il circuito di un codificatore è composto da sole porte `OR`.

>[!warning] Coder 4-2:
>![[IMG_1D687B81F39F-1.jpeg|600]]

>[!warning] Coder 8-2
>![[IMG_2596.jpeg|600]]
