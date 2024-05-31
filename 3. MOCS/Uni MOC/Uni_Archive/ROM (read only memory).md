---
created: 2024-02-02
type: Uni Note
class:
  - "[[Programmazione Calcolatori (Class)]]"
academic year: 2023/2024
related:
  - "[[Circuiti combinatori]]"
completed: true
updated: 2024-05-27T13:29
---
---
## Indice
1. [[#Definizione]]
2. [[#Funzionamento]]
3. [[#Circuito + Esempio]]

---
## Definizione

É un **circuito combinatorio** composto da un [[Circuito De-codificatore|decodificatore]] e da un [[Circuito Codificatore|codificatore]] in cascata.
- *Decodificatore:* matrice porte **and** le cui entrate sono gli input della ROM
- *Codificatore:* matrice porte **or** le cui uscite sono output della ROM

>[!tip] Significato del nome
>Il nome Read Only Memory deriva dal fatto che la ROM può essere vista come una memoria non riscrivibile (di sola lettura). Infatti, è costituita di celle di dimensione fissata, ognuna con il proprio indirizzo (11, 10...), come una memoria, ma una volta saldati i diodi i valori memorizzati non possono essere cambiati se non creando un nuovo circuito.
 
---
## Funzionamento
- Il decoder genera tutti i possibili mintermini
- I mintermini vengono selezionati attraverso l'array di porte or
- Uscite delle porte or non sono altro che l'output della rom

---
## Circuito + Esempio

![[Pasted image 20240203105207.png|800]]

---