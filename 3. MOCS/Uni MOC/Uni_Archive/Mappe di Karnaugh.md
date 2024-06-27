---
created: 2023-10-23
type: Uni Note
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
academic year: 2023/2024
related:
  - "[[Algebra Booleana]]"
  - "[[Tabelle di verità, Maxtermini e Mintermini]]"
completed: true
updated: 2024-06-27T23:32
---
>[!abstract] Index
>1. [[#Introduzione]]
>2. [[#Come creare mappa di Karnaugh]]
>3. [[#Semplificazione]]
>4. [[#Esempi]]

>[!abstract] Related
>- [[Algebra Booleana]]
>- [[Progettazione Sistemi Digitali (class)]]

---
## Introduzione

>[!note] Definizione
>- Metodo semplificativo per funzioni logiche.
>- Garantisce la massima semplificazione (secondo la Prof. Massini)
>- Non garantisce la massima semplificazione (secondo il Prof. Simonetta).
>- Consigliato usare massimo 4 variabili.

>[!tip] Tip
>**Pos:** P --> Primo = `0` --> Raccogliere `0`
>**Sop:** S --> Secondo  = `1` --> Raccogliere `1`

---
## Come creare mappa di Karnaugh

>[!note] Struttura della mappa
>![[IMG_0C9357783BF9-1.jpeg|800]]

>[!note] Tabella di verità-->Mappa K
>![[IMG_5F2A185DC9A7-1.jpeg|600]]

---
## Semplificazione

>[!note] Quando si raccoglie si deve
>1. Creare gruppi composti da $2^n$ elementi
>2. Creare gruppi più grandi possibili 
>3. Fare il minor numero di gruppi
>4. Quando è possibile non fare overlapping 

>[!warning] Froma Pos
>Raccogliendo per 0 si trovano i [[Tabelle di verità, Maxtermini e Mintermini#Max-termine (0)|maxtermini]] che verranno uniti da or (risultato forma *pos*)
>
>![[IMG_41CF323F2323-1.jpeg|800]]

>[!warning] Forma Sop
>Raccogliendo per 1 si trovano i [[Tabelle di verità, Maxtermini e Mintermini#Min-termine (1)|mintermine]] che verranno uniti da and (risultato forma *sop*)
>
>![[IMG_A1F23F894B21-1.jpeg|800]]

---
## Esempi

![[IMG_D25867EC0D16-1.jpeg|600]]
