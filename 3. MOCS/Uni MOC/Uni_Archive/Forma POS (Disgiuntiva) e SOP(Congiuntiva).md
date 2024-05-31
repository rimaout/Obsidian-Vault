---
created: 2023-11-27
type: Uni Note
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
academic year: 2023/2024
related:
  - "[[Algebra Booleana]]"
completed: true
updated: 2024-05-27T13:29
---
---
## Indice
1. [[#Definizione]]
2. [[#Conversioni]]

---
## Definizione

**POS (product of sums):** 
- ***Forma Disgiuntiva***
- Per forma pos si intende una funzione booleana scritta come prodotti di somme
- Ovvero termini prodotto uniti da somme logiche  

**SOP (sum of products):** 
- ***Forma Congiuntiva***
- Per forma sop si intende una funzione booleana scritta come somma di prodotti
- Ovvero termini somma uniti da prodotti logici logiche  

---
## Conversioni

**Legge di Demorgan:** 
1. Negare due volte l'espressione
2. Applicare demorgan su negazione più interna
3. Semplificare ed eseguire operazioni
4. Applicare di nuovo demorgan su negazione più esterna

**Dualità di una funzione booleana**
- Un espressione booleana *E1* è la duale di una espressione *E2* se 
	- Differisce per gli operatori (and e or sono scambiati)
	- Il valore delle costanti (0 e 1 sono scambiati)
	
- Passare all'espressione duale di un'identità può facilitare:
	- la verifica dell'identità
	- Convertire dalla forma sop a pos

>[!warning] Oss:
>- Per passare da **pos** a **sop** basta applicare proprietà distributiva

**Esempio:**
![[soppos.jpeg|800]]

---