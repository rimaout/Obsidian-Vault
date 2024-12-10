---
type: Uni Note
class:
  - "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related:
  - "[[Interruzioni 101]]"
completed: true
created: 2024-09-28T12:03
updated: 2024-12-09T16:14
---

>[!abstract] Related
>- [[Interruzioni 101]]
>- [[Sistemi Operativi 1 (class)]]

---
## Gestione dell' Input Output

L'I/O è il processo mediante il quale un sistema informatico interagisce con l'esterno, scambiando dati con dispositivi come tastiere, schermi, dischi e così via.

Esistono tre modi principali in cui un sistema informatico può gestire l'I/O: 

>[!note] I/O Programmato
>- Metodo più semplice e primitivo di gestione dell'I/O. 
>- L’azione di lettura o scrittura viene effettuata da un modulo dedicato (non il processore). 
>- Non essendoci, interruzioni il processore deve attendere (inutilizzato) che l'operazione di I/O sia completata prima di poter proseguire con le istruzioni successive (**Busy Waiting**).
>
>Questo approccio è lento e inefficiente, poiché il processore è bloccato durante l'attesa dell'operazione di I/O.

>[!note] I/O da Interruzioni
>- Metodo più moderno per la gestione dell'I/O. 
>- In questo approccio, quando un dispositivo di I/O è pronto per lo scambio di dati, invia un segnale di interruzione al processore. 
>- Il processore interrompe l'esecuzione delle istruzioni e salva lo stato attuale, esegue un'apposita routine di gestione dell'interruzione, chiamata gestore di interruzione.
>- Quando l'operazione di I/O è completata completata, il processore riprende l'esecuzione delle istruzioni. 
> 
>Questo approccio è più efficiente dell'I/O programmato, poiché il processore non è bloccato durante l'attesa dell'operazione di I/O.
>
>**Related:** [[Interruzioni 101]]

>[!note] I/O con accesso diretto in memoria (DMA)
>- Metodo Più efficiente per la gestione dell'I/O.
>- In questo approccio, un controller di I/O speciale, chiamato controller DMA, gestisce l'operazione di I/O senza l'intervento del processore.
>- Il controller DMA legge o scrive dati direttamente nella memoria del sistema, senza dover passare attraverso il processore. 
>- Il processore viene interrotto soltanto al termine del trasferimento.
>
>Questo approccio è molto più veloce dell'I/O programmato e dell'I/O da interruzioni, poiché il processore non è coinvolto nell'operazione di I/O.

^d3d6d0

![[1721y32yuh327y.png]]