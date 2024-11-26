---
type: Uni Note
class: "[[Basi di Dati 1 (class)]]"
academic year: 2024/2025
related: 
completed: false
created: 2024-11-25T09:41
updated: 2024-11-25T09:49
---
>[!abstract] Related
>- 

---
## Introduzione

Come abbiamo visto una [[Decomposizione di uno schema relazionale|decomposizione]] deve rispettare queste 3 condizioni:
1. Ogni *sotto-schema* deve essere *3NF*
2. La decomposizione deve *preservare le dipendenze funzionali*
3. deve essere possibile ricostruire ogni istanza legale dello schema originale tramite join naturale di istanze della decomposizione

Abbiamo anche visto come [[Decomposizione con Join senza Perdita (Verifica)|verificare]] che una decomposizione rispetti queste regola, ma non abbiamo ancora visto come calcolare una decomposizione valida.

>[!warning] Sempre possibile ?
>***Si***, è sempre possibile.


---
## Algoritmo 

La decomposizione che si ottiene dall’algoritmo che studieremo non è l’unica possibile che soddisfi le condizioni richieste. Lo stesso algoritmo, a seconda dell’input di partenza (di cui parleremo in questa lezione) può fornire risultati diversi e tuttavia corretti.

Prima di continuare dobbiamo introdurre il concetto di «[[Copertura Minimale|copertura minimale]]» di un insieme F di dipendenze funzionali.
