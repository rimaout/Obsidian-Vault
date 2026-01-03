---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: true
created: 2025-02-07T22:44
updated: 2025-02-08T11:45
---
Le liste sono strutture dati che implementano l'interfaccia `List` e memorizzano i dati in modo sequenziale e dinamico. Ciò significa che le liste possono aumentare o diminuire la loro dimensione in base alle esigenze.

Le liste più utilizzate sono [[#ArrayList]] e [[#LinkedList]].

### ArrayList

L'`ArrayList` è una struttura dati ad accesso casuale che permette di accedere direttamente a ogni elemento della lista. È implementata attraverso un array a cui è stata aggiunta una funzionalità di ridimensionamento automatico.

Caratteristiche dell'`ArrayList`:
*   **Accesso casuale**: è possibile accedere direttamente a ogni elemento della lista.
*   **Ridimensionamento automatico**: aumentano o diminuiscono automaticamente la dimensione dell'array sottostante per fare spazio a nuovi elementi o liberare spazio.

### LInkedList

In una `LinkedList`, ogni elemento è rappresentato da un nodo che contiene un valore e un riferimento al nodo successivo. 

Caratteristiche della `LinkedList`:
- **Accesso sequenziale**: non sono ad accesso casuale, ma ad accesso sequenziale. Ciò significa che per accedere a un elemento, si deve prima passare per tutti i suoi precedenti.
- **Inserimento e rimozione**: le `LinkedList` sono utili perché permettono di aggiungere o rimuovere un nodo alla lista senza dover rilocare tutta la struttura dati.

Svantaggi della `LinkedList`
- **Accesso lento**: tempi di accesso più lenti rispetto ad altre strutture dati, a causa della necessità di scorrere la lista per accedere a un elemento.
- **Memoria aggiuntiva**: le `LinkedList` richiedono memoria aggiuntiva per i riferimenti ai nodi successivi

>***oss:*** `LinkedList` implementa anche l'interfaccia [[Java - Queue & Stack|queue]] (coda).