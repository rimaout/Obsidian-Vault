---
created: 2023-11-07
type: Uni Note
class:
  - "[[Progettazione Sistemi Digitali (class)]]"
academic year: 2023/2024
related:
  - "[[Circuiti Sequenziali]]"
completed: true
updated: 2024-06-25T12:29
---
---

>[!abstract] Related
>- [[Circuiti Sequenziali]]
>- [[Progettazione Sistemi Digitali (class)]]

---
## Circuiti Sincroni

I **Sistemi sincroni** sono circuiti in cui per far si che si passi dallo stato **presente** allo stato **futuro** si utilizza un impulso di clock.
Quindi la velocità di risposta del sistema è condizionata dalla frequenza di clock.

>[!warning] Segnale di Clock
>Un segnale di clock è un **segnale periodico** che fornisce un riferimento temporale per le operazioni del sistema, consentendo ai componenti di eseguire le loro funzioni in modo coordinato e sincronizzato.

## Circuiti Asincroni

I circuiti asincroni possono permettere velocità maggiori dei circuiti sincroni, in quanto non sono limitati dal segnale di clock.

Nei circuiti asincroni l'evoluzione avviene solo per commutazione degli ingressi, questi determinano i livelli delle grandezza del circuiti e, quando sono terminati i transitori di commutazione e il circuito ha raggiunto uno stato stabile, si può permettere una nuova commutazione degli ingressi, senza attendere il segnale di clock.

I circuiti sequenziali asincroni sono impiegati inoltre per connettere dispositivi che non sono sincronizzati da uno stesso segnale di clock. Occorre però verificare che non esistano stati non utilizzati che, causa di disturbi o malfunzionamenti del circuito, divengano stati di blocco del circuito stesso.