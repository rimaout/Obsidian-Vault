---
created: 2023-10-16
type: Uni Note
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
academic year: 2023/2024
related:
  - "[[Algebra Booleana]]"
  - "[[Forma POS (Disgiuntiva) e SOP(Congiuntiva)]]"
completed: true
updated: 2024-05-27T13:29
---
---
## Index
1. [[#Tavola di verità]]
2. [[#Min-termine]]
3. [[#Max-termine]]

>[!danger] Oss:
>*P*os: *P* --> *P*rimo = **0** --> Raccogliere **0**
>*S*op: *S*op --> *S*econdo  = **1** --> Raccogliere **1**

>[!danger] Oss:
>- Raccogliendo **0** otteniamo **maxtermini** uniti da and
>- Raccogliendo **1** otteniamo **mintermini** uniti da or

---
## Tavola di verità
**Definizione:**
- Una tabella della verità specifica la relazione che esiste tra il valore della variabili in ingresso e i risultati della funzione

**Come costruire tabella di verità:**
- Si devono rappresentare tutte le possibili combinazioni che esistono tra le variabili in ingresso 

![[IMG_D0366012EE96-1.jpeg|400]]

---
## Min-termine (1)
**Definizione:** Un *termine prodotto* in cui compaiono letterali corrispondenti a tutte le variabili della funzione e tale per cui la configurazione di valori delle variabili definite dai letterali *genera un valore 1* della funzione stessa nella tabella delle verità, costituisce un mintermine della funzione

**oss:** se valore variabile = *0* allora nel mintermine la variabile è *negata*

**Calcolo funzione:** Unire mintermini con somme logiche ([[Forma POS (Disgiuntiva) e SOP(Congiuntiva)|forma sop]])
![[IMG_CB75ECEBC666-1.jpeg|400]]

---
## Max-termine (0)
**Definizione:** Un *termine somma* in cui compaiono letterali corrispondenti a tutte le variabili della funzione e tale per cui la configurazione di valori delle variabili definite dai letterali *genera un valore 1* della funzione stessa nella tabella delle verità, costituisce un mintermine della funzione

**oss:** se valore variabile = *1* allora nel mintermine la variabile è *negata*

**Calcolo funzione:** Unire mintermini con somme logiche ([[Forma POS (Disgiuntiva) e SOP(Congiuntiva)|forma sop]])

![[IMG_5DD59C7AAC59-1.jpeg|400]]

---