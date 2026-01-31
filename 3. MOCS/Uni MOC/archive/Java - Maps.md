---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: true
created: 2025-02-07T19:05
updated: 2026-01-31T13:32
---
Sono strutture dati che *implementano l'interfaccia* `Map` ed organizzano i dati in coppie chiave-valore, dove non possono esistere due elementi con la stessa chiave.

Di base le mappe non implementano iterable e quindi non è possibile iterarci, ma è comunque possibile ottenere il set delle chiavi ed il set dei valori su cui poi è possibile iterare.

>[!note] Multi Mappa
>
>Una multi mappa è una mappa che permette di memorizzare più valori a frontedella stessa chiave

#### HashMap

Memorizzati le coppie chiave-valore in una [[Java - Sets#^3a11b6|tabella di hash]], dove la chiave è utilizzata per calcolare la posizione nella tabella attraverso una funzione di hash. Questo assicura velocità di inserimento e ricerca ottime.

Per funzionare correttamente, la chiave deve implementare i metodi `equals()` e `hashCode()` in modo appropriato. Il metodo `hashCode()` è utilizzato per calcolare l'indice della tabella di hash dove memorizzare il valore associato alla chiave, mentre il metodo `equals()` è utilizzato per verificare se due chiavi sono uguali.

#### TreeMap

Memorizza le coppie chiave-valore in una struttura ad [[Java - Sets#^6a39b8|albero]], che mantiene un ordinamento naturale rispetto alle chiavi.

#### LinkedHashMap

Memorizza le coppie chiave-valore in una tabella hash proprio come un [[#HashMap]] ma allo stesso tempo mantiene una copia dei dati in una struttura simile ad una [[Java - Lists#LinkedList|LinkedList]].

Questo permette di avere le prestazioni del [[#HashMap]] e allo stesso tempo mantenere l'ordinamento di inserimento attraverso la [[Java - Lists#LinkedList|LinkedList]].

Naturalmente questa struttura dati richiede più memoria ed overHead per il mantenimento della due strutture dati.

