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
updated: 2024-05-27T13:29
---
---
## Index
1. [[#Definizione]]
2. [[#Circuito]]

---
## Definizione
È utilizzato per decodificare gli output di un [[Circuito Codificatore]]

>[!warning] Rappresentazione circuitale
>![[Pasted image 20240131163252.png|150]]

>[!danger] Caratteristiche
>- È un [[Circuiti combinatori|circuito combinatorio]]
>- $n$ inputs --> $n^2$ outputs
>- La funzione del [[Circuito De-codificatore]] è l'opposta del [[Circuito Codificatore]]

>[!danger] Funzionamento
>- Le linee in uscita saranno tutte 0 tranne quella nella posizione espressa (in binario) dalle linee di input

>[!warning] oss:
>De-codificatore = *Array porte AND*

---
## Circuito

>[!warning]
>Codificatore = *Array porte OR*
>- Circuito decodificatore si può vare sono con **AND** forma [[Forma POS (Disgiuntiva) e SOP(Congiuntiva)|Congiuntiva (POS)]]

**Tabella verità --> Circuito:**
- Vediamo out put quando è uno:
	- cerchiamo variabili che lo rendono 1 solo in quel caso

*Decoder 2-4:*
![[IMG_2598.jpeg|600]]

*Decoder 3-8:*
![[IMG_2599.jpeg|600]]

---
