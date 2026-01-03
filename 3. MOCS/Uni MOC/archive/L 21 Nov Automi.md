---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2025-11-21T09:21
updated: 2025-11-21T09:39
---
Adesso studieremo il calcolo della complessità di un algoritmo, ovvero l'utilizzo di risorse di una macchina di Turing.

- anche se esistono altri tipi di risorse utilizzato d aun algoritmo noi vedremo, tempo e spazio.


---
Esempio:

I linguaggio $\text{PATH = } \{ <G, s, t>: \exists s \leadsto t \{  G \text{ Grafo} \}, s \text{ e }t \text{ nodi} \}$
...

---
Inoltre esistono molti problemi della **Teoria della complessità** che non sono ancora stati risolti:
- P = NP ovvero esiste un problema in cui trovare una soluzione è più efficiente che trovarla.
- P = PSpace ovvero se puoi risolvere un problema in poco spazio è possibile risolverlo anche in poco tempo?
- P = BPP ovvero ogni algoritmo efficiente, può essere de-randomizzato

---
**Definizione** di complessità di tempo (in un caso deterministico)

Sia M un TM decisore, allora la complessità di tempo di M è $T: \mathbb{N} \to \mathbb{N}$ t.c. $T(n) = \max_{x \in \Sigma^{*}} \{ \text{\# passi richiesti da }M(x) \}$

Vogliamo capire come la funzione si comporta in termini di grandezza dell'input