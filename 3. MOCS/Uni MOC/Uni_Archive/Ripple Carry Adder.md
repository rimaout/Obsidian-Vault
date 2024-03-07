---
Created: 2024-02-04
Type: Uni Note
Class:
  - "[[Progettazione Sistemi Digitali (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Circuiti Aritmetici]]"
  - "[[Circuiti combinatori]]"
Completed: true
---
## Index
1. [[#Definizione]]
2. [[#Circuito]]
3. [[#Ritardo]]
4. [[#Sottrazione con Ripple Carry Adder]]

---
## Definizione
Il **Ripple Carry Adder (RCA)** è un circuito che esegue la somma tra due numeri binari di n bit.

>[!warning] Struttura:
>Il RCA è composto da:
>- 1 [[Half-Adder]] (che si occupa di sommare i bit meno significativi)
>- n-1 [[Full-Adder]]
>
>Messi in cascata dal meno significativo al più significativo con l'uscita riporto (c) è connessa all'entrata riporto (cin) del successivo.

---
## Circuito
La composizione gerarchica dell'RCA consente la semplificazione della progettazione di un circuito sommatore di numeri a n bit. Ad esempio la somma di due numeri a 4 bit richiederebbe la semplificazione di una tabella di 256 righe (8 variabili in entrata).

>[!warning] Circuito
![[Pasted image 20240204143538.png|700]]

>[!warning] oss
>![[Pasted image 20240204120600.png|300]]

---
## Ritardo 
Quando si crea un circuito in cascata come questo è inevitabile che si crei del ritardo, infatti ogni adder deve aspettare il riporto del adder precedente per poter effettuare l'operazione.

---
## Sottrazione con Ripple Carry Adder
![[Sottrazione con Ripple Carry Adder]]