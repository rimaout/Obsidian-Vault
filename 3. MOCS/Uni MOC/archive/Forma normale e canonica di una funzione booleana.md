---
created: 2023-10-16
type: Uni Note
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
academic year: 2023/2024
related:
  - "[[Tabelle di verità, Maxtermini e Mintermini]]"
  - "[[Algebra Booleana]]"
completed: true
updated: 2026-01-31T13:32
---
>[!abstract] Index
>1. [[#Forma normale]]
>2. [[#Come ottenere forma normale]]
>3. [[#Forma canonica]]
>4. [[#Come ottenere forma canonica]]
>5. [[#Consigli]]

>[!abstract] Related
>- [[Algebra Booleana]]
>- [[Progettazione Sistemi Digitali (class)]]

---
## Forma normale 

>[!note] Sop (forma normale disgiuntiva)
>- rete: and-to-or

>[!note] Pos (forma normale congiuntiva)
>- rete: or-to-and

>**OSS:** forma normale != [[Circuito ed espressione minimale|forma minimale]]

#### Come ottenere forma normale

>[!warning] Metodo
>1. Applicare leggi di demorgan (fino ad ottenere la complementazione sulle singole variabili)
>2. Proprietà distributiva
>3. Eliminare termini ripetuti (usare idempotenza)

---
## Forma canonica

>[!note] Sop (forma canonica disgiuntiva)
>- Tutti i termini prodotto sono min-termini

>[!note] Pos (forma canonica congiuntiva)
>- tutti i termini somma sono max-termini

#### Come ottenere forma canonica

>[!note] Forma normale --> Forma canonica
>>**Forma canonica SOP:** 
>>- Moltiplicare il termine prodotto in cui manca x per (x+!x)
>>		![[IMG_2594.jpeg|600]]
>	
>>**Forma canonica POS:**
>>- sommare al termine somma in cui manca x il prodotto x!x
>>		![[IMG_2593.jpeg|600]]

>[!note] Tabella di verità --> Forma canonica
>
>>[!warning] Forma canonica SOP
>>- Calcolare la funzione trovando i mintermini:
>>	![[Tabelle di verità, Maxtermini e Mintermini#Min-termine (1)]]
>
>>[!warning] Forma canonica POS
>>- Calcolare la funzione trovando i max-termini: 
>>![[Tabelle di verità, Maxtermini e Mintermini#Max-termine (0)]]

---
## Consigli

![[IMG_5ABE40527815-1.jpeg]]