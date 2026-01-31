---
created: 2023-10-16
type: Uni Note
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
academic year: 2023/2024
related:
  - "[[Algebra Booleana]]"
  - "[[Forma POS (Congiuntiva) e SOP (Disgiuntiva)]]"
completed: true
updated: 2026-01-31T13:32
---
>[!abstract] Index
>1. [[#Tavola di verità]]
>2. [[#Min-termine (1)]]
>3. [[#Max-termine (0)]]
>4. [[#Consigli]]

>[!abstract] Related
>- [[Algebra Booleana]]
>- [[Progettazione Sistemi Digitali (class)]]

---
## Tavola di verità

>[!note] Definizione
>Una tabella della verità specifica la relazione che esiste tra il valore della variabili in ingresso e i risultati della funzione

>[!note] Come costruire tabella di verità
>- Si devono rappresentare tutte le possibili combinazioni che esistono tra le variabili in ingresso 
>
>![[IMG_D0366012EE96-1.jpeg|400]]

---
## Min-termine (1)

>[!note] Definizione
>Un *termine prodotto* in cui compaiono letterali corrispondenti a tutte le variabili della funzione e tale per cui la configurazione di valori delle variabili definite dai letterali *genera un valore 1* della funzione stessa nella tabella delle verità, costituisce un mintermine della funzione

>**OSS:** se valore variabile = *0* allora nel mintermine la variabile è *negata*

>[!note] Calcolo funzione 
>Unire mintermini con somme logiche ([[Forma POS (Congiuntiva) e SOP (Disgiuntiva)|forma sop]])
>![[IMG_CB75ECEBC666-1.jpeg|400]]

---
## Max-termine (0)

>[!note] Definizione
>Un *termine somma* in cui compaiono letterali corrispondenti a tutte le variabili della funzione e tale per cui la configurazione di valori delle variabili definite dai letterali *genera un valore 1* della funzione stessa nella tabella delle verità, costituisce un mintermine della funzione

>**OSS:** se valore variabile = *1* allora nel mintermine la variabile è *negata*

>[!note] Calcolo funzione
>Unire mintermini con somme logiche ([[Forma POS (Congiuntiva) e SOP (Disgiuntiva)|forma sop]])
>
>![[IMG_5DD59C7AAC59-1.jpeg|400]]

---
## Consigli

>[!tip] Come ricordare cosa raccogliere ? 
>- **Pos:** `P` --> *P*rimo = `0` --> Raccogliere `0`
>- **Sop:** `S` --> *S*econdo  = `1` --> Raccogliere `1`

>[!warning] Max e Min Termini
>- Raccogliendo **0** otteniamo **maxtermini** uniti da and
>- Raccogliendo **1** otteniamo **mintermini** uniti da or