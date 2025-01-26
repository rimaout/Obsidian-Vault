---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-01-20T16:49
updated: 2025-01-20T20:01
---
## MVC

Il progetto segue il modello MVC (Model, View e Controller), che permette di non avere dipendenze tra il modello, assicurando che sia al 100% riutilizzabile.

Questa struttura è suddivisa in tre package:

* `Model`: in cui è presente tutta la logica del gioco, come nemici, player, mappe ecc. Il modello rappresenta i dati del gioco e gestisce le regole del gioco.
* `View`: si occupa di rappresentare a schermo i veri elementi del gioco. La view riceve i dati dal modello e li rappresenta in una forma visiva.
* `Controller`: si occupa di interpretare gli input provenienti dall'utente e di comunicare con il modello e la view. Il controller gestisce gli input dell'utente e aggiorna i dati del modello.

Per assicurare l'indipendenza del modello dagli altri due package, quest'ultimo non accede mai ad alcuna informazione o metodo presente al di fuori di sé stesso.

Al contrario, `Controller` e `View` sono completamente dipendenti dal `Model` per il loro funzionamento.

Il modello MVC offre diversi vantaggi, tra cui la separazione della logica del gioco dalla rappresentazione visiva e la riduzione delle dipendenze tra le diverse componenti del progetto. Ciò rende più facile la manutenzione e la modifica del codice e permette di riutilizzare il codice in altri progetti.

#### Difficoltà

Implementare una completa separazione tra model, view e controller non è semplice, specialmente quando abbiamo che il model deve notificare un suo cambio di stato agli altri componenti. Per fare ciò è possibile utilizzare il design pattern **Observer Observable**.

