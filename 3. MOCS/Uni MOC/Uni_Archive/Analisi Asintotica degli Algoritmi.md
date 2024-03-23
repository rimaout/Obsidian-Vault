---
Created: 2024-02-26
Type: Uni Note
Class:
  - "[[Algoritmi 1 (class)]]"
Academic Year: 2023/2024
Related:
  - "[[Complessità Algoritmica]]"
Completed: true
---
---

>[!info] Index
>1. 
>2. [[#Notazione asintotica]]
>	- [[Notazione Big O (O)]]
>	- [[Notazione Omega (Ω)]]
>	- [[Notazione Theta (Θ)]]
>3. [[#Grafico della complessità algoritmica]]
>4. [[#Teoremi]]
>

---
## Introduzione

L'esecuzione di un qualsiasi programma (algoritmo) ha un costo in termini di:
- **Complessità Spaziale** (utilizzo di memoria)
- **Complessità Temporale** (tempo di esecuzione)

Queste complessità possono variare all'aumentare al aumentare della dimensione dei dati in input.

Per studiare le complessità di un algoritmo si utilizza il metodo dell'[[Analisi Asintotica degli Algoritmi]].

---
## Notazione asintotica 

**In matematica** la notazione asintotica permette di confrontare il tasso di crescita (comportamento asintotico) di una funzione nei confronti di un’altra.

**In informatica** il calcolo asintotico è utilizzato per analizzare la complessità di un algoritmo.
In particolare modo, per stimare quanto aumenta il tempo di esecuzione al crescere della dimensione dell’input.

Le notazioni asintotiche più comunemente utilizzate sono:
- **[[Notazione Big O (O)]]** è il limite superiore asintotico
- **[[Notazione Omega (Ω)]]** è il limite inferiore asintotico
- **[[Notazione Theta (Θ)]]** è il limite asintotico stretto
 
Utilizzando la notazione asintotica, possiamo confrontare diversi algoritmi e scegliere quello più efficiente per un dato problema.

---
## Grafico della complessità algoritmica

![[Pasted image 20240306160913.png]]

>[!warning] oss
>Nota che le funzioni che ci interessano catturano tempi di esecuzione degli algoritmi e sono quindi sono non negative, pertanto il vincolo dell’asintoticità non negativa non ci fa perdere di generalità.

---
## Teoremi

1. [[#^fd7e3b|Regole sulle costanti moltiplicative]]
2. [[#^874e2f|Regole sulla combattività con la somma]]
3. [[#^aa3bf0|Regole sulla combattività com il prodotto]]

>[!warning] Altre osservazioni utili:
>- [[Qualunque logaritmo è dominato da una radice (notazione asintotica)]]

---
##### Regole sulle costanti moltiplicative
^fd7e3b

![[Pasted image 20240306172732.png|600]]

>[!warning] Informalmente
>Le costanti moltiplicative si possono ignorare

---
##### Regole sulla combattività con la somma
^874e2f
![[Pasted image 20240306172850.png|600]]

>[!warning] Informalmente
>Le notazioni asintotiche commutano con l’operazione somma.

---
##### Regole sulla combattività com il prodotto
^aa3bf0

![[Pasted image 20240306172911.png|600]]

>[!warning] Informalmente
>Le notazioni asintotiche commutano con l’operazione prodotto.
