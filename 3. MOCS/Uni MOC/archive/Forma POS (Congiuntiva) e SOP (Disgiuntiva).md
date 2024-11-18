---
created: 2023-11-27
type: Uni Note
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
academic year: 2023/2024
related:
  - "[[Algebra Booleana]]"
completed: true
updated: 2024-06-27T20:16
---
>[!abstract] Index
>1. [[#Definizione]]
>2. [[#Conversioni]]

>[!abstract] Related
>- [[Algebra Booleana]]
>- [[Progettazione Sistemi Digitali (class)]]

---
## Definizione

>[!note] POS (product of sums)
>- **Forma Congiuntiva**
>- **Significato:** Funzione booleana scritta come prodotti di somme
>	- Ovvero termini prodotto uniti da somme logiche  

>[!note] SOP (sum of products)
>- **Forma Disgiuntiva**
>- **Significato:** Funzione booleana scritta come somma di prodotti
>	- Ovvero termini somma uniti da prodotti logici logiche  

---
## Conversioni

>[!note] Legge di Demorgan
>1. Negare due volte l'espressione
>2. Applicare demorgan su negazione più interna
>3. Semplificare ed eseguire operazioni
>4. Applicare di nuovo demorgan su negazione più esterna

>[!note] Dualità di una funzione booleana
>- Un espressione booleana *E1* è la duale di una espressione *E2* se 
>	- Differisce per gli operatori (and e or sono scambiati)
>	- Il valore delle costanti (0 e 1 sono scambiati)
>	
>- Passare all'espressione duale di un'identità può facilitare:
>	- la verifica dell'identità
>	- Convertire dalla forma sop a pos


>**OSS:** Per passare da **pos** a **sop** basta applicare proprietà distributiva

>[!warning] Esempio
>![[soppos.jpeg|800]]

