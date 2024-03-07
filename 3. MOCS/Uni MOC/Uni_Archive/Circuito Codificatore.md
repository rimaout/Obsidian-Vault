---
Created: 2023-10-29
Type: Uni Note
Class:
  - "[[Progettazione Sistemi Digitali (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Circuiti combinatori]]"
  - "[[Circuito De-codificatore]]"
Completed: true
---
---
## Index
1. [[#Definizione]]
2. [[#Codificatore standard e non standard]]
3. [[#Esempi]]

---
## Definizione
È un [[Circuiti combinatori|circuito combinatorio]] utilizzato principalmente per ridurre il numero di linee di dati

>[!warning] Rappresentazione circuitale
>![[Pasted image 20240131163117.png|150]]

>[!danger] Caratteristiche
>- È un circuito [[Circuiti combinatori|circuito combinatorio]]
>- $n^2$ (o meno) inputs --> $n$ outputs
>- La funzione del [[Circuito Codificatore]] è l'opposta al [[Circuito De-codificatore]]

>[!danger] Funzionamento 
> Le linee in uscita danno la posizione (espressa in binario) dell'unica variabile in input con valore 1.
> 
*oss:* Si assume che in qualsiasi condizione, ci sia soltanto un ingresso che valga 1.

>[!warning] oss:
>Codificatore = *Array porte OR*

---
## Codificatore standard e non standard
- **Codificatore standard:** utilizza il massimo numero di input rappresentabili dall'output e i numeri binari delle uscite corrispondono al pedice dell'entrata che vale 1
	- *Esempio:* 3 output, input 8 

- **Codificatore non standard:** non utilizza il massimo numero di input rappresentabili dall'output o i numeri binari delle uscite non corrispondono al pedice dell'entrata che vale 1
	- *Esempio:* 3 output , 5 input

>[!warning] oss:
>- 3 output = max 8 input ($2^3$)

---
## Circuito

>[!warning]
>Codificatore = *Array porte OR*
>- Circuito codificatore si può fare sono con **OR** forma [[Forma POS (Disgiuntiva) e SOP(Congiuntiva)|Disgiuntiva (SOP)]]

**Tabella verità --> Circuito:**
- Vediamo out put e cerchiamo gli input che se sommati tra loro ci danno output.

*Coder 4-2:*
![[IMG_1D687B81F39F-1.jpeg|600]]

*Coder 8-2:*
![[IMG_2596.jpeg|600]]

---