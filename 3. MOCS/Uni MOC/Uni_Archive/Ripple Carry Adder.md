---
created: 2024-02-04
type: Uni Note
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
academic year: 2023/2024
related:
  - "[[Circuiti Aritmetici]]"
  - "[[Circuiti Combinatori]]"
completed: true
updated: 2024-06-14T11:00
---

>[!abstract] Index
>1. [[#Introduzione]]
>2. [[#Circuito]]
>3. [[#Ritardo]]

>[!abstract] Related
>- [[Circuiti Aritmetici]]
>- [[Circuiti Combinatori]]
>- [[Progettazione Sistemi Digitali (class)]]

---
## Introduzione

Il **Ripple Carry Adder (RCA)** è un circuito che esegue la somma tra due numeri binari di `n` bit.

>[!warning] Struttura
>Il RCA è composto da:
>- `1` [[Half-Adder]]
>- `n-1` [[Full-Adder]]
>
>Messi in cascata dal meno significativo al più significativo con l'uscita riporto (c) è connessa all'entrata riporto (cin) del successivo.

>**Vedi:** [[Sottrazione con Ripple Carry Adder]]

---
## Circuito

La composizione gerarchica dell'RCA consente la semplificazione della progettazione di un circuito sommatore di numeri a `n` bit. Ad esempio la somma di due numeri a 4 bit richiederebbe la semplificazione di una tabella di 256 righe (8 variabili in entrata).

>[!warning] Circuito
>![[Pasted image 20240204143538.png|700]]

>[!warning] oss
>![[Pasted image 20240204120600.png|300]]

---
## Ritardo 

Quando si crea un circuito in cascata come questo è inevitabile che si crei del ritardo, infatti ogni adder deve aspettare il riporto del adder precedente per poter effettuare l'operazione.