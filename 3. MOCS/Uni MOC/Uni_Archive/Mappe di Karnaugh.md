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
updated: 2024-05-27T13:29
---
---
## Index
1. [[#Definizione]]
2. [[#Come creare mappa di Karnaugh]]
3. [[#Semplificazione]]
4. [[#Esempi]]

>[!warning] Oss:
>*P*os: *P* --> *P*rimo = **0** --> Raccogliere **0**
>*S*op: *S*op --> *S*econdo  = **1** --> Raccogliere **1**
---

---
## Definizione
- Metodo semplificativo per funzioni logiche 
- Garantisce la massima semplificazione (secondo la Massini), Non garantisce la massima semplificazione (secondo il Simonetta)
- Consigliato usare massimo 4 variabili

---
## Come creare mappa di Karnaugh
1. **Struttura della mappa**
![[IMG_0C9357783BF9-1.jpeg|1000]]

2. **Tabella di verità-->Mappa K:**
![[IMG_5F2A185DC9A7-1.jpeg|700]]

---
## Semplificazione

***Quando si raccoglie si deve:***
1. Creare gruppi composti da $2^n$ elementi
2. Creare gruppi più grandi possibili 
3. Fare il minor numero di gruppi
4. Quando è possibile non fare overlapping 

***Froma Pos:***
Raccogliendo per 0 si trovano i [[Tabelle di verità, Maxtermini e Mintermini#Max-termine (0)|maxtermini]] che verranno uniti da or (risultato forma *pos*)

![[IMG_41CF323F2323-1.jpeg|800]]

***Forma Sop:***
Raccogliendo per 1 si trovano i [[Tabelle di verità, Maxtermini e Mintermini#Min-termine (1)|mintermine]] che verranno uniti da and (risultato forma *sop*)

![[IMG_A1F23F894B21-1.jpeg|800]]

---
## Esempi

![[IMG_D25867EC0D16-1.jpeg|700]]

---