---
type: Uni Note
class: "[[Basi di Dati 1 (class)]]"
academic year: 2024/2025
related:
  - "[[Introduzione all'organizzazioni dei database]]"
completed: false
created: 2024-12-04T11:50
updated: 2024-12-04T12:25
---
>[!abstract] Related
>- [[Introduzione all'organizzazioni dei database]]
>- [[Basi di Dati 1 (class)]]

---
## Introduzione

Questo tipo di file è suddiviso in **bucket** numerati da 0 a B-1, ciascun bucket è costituito da uno o più blocchi collegati fra loro tramite puntatori e organizzati come un heap. In cima al file c’è la **bucket directory** che contiene tutti i puntatori per i bucket ovvero B elementi.

---
## Funzione Hash

Dato un valore _v_ per la chiave, il numero del bucket in cui deve trovarsi un record con chiave _v_ è calcolato mediante una funzione chiamata **funzione hash**.

Una funzione di Hash per essere “buona” deve suddividere in modo equo i record nei vari bucket, quindi al variare della chiave tutti i bucket devono avere la stessa probabilità di “uscita”. 

***Funzionamento:*** In genere una funzione hash trasforma la chiave in un numero, lo divide per B e fornisce il resto della divisione come numero del bucket (in modo da rimanere limitati al numero di bucket), questo resto è il bucket dove andrà inserito il record.

>[!example] Esempio
>
>Trattiamo il valore _v_ della chiave come una sequenza di bit, ad esempio $100101111010$, dividiamo tale sequenza in gruppi di bit uguali fra loro e sommiamo tali gruppi come se fossero interi:
>
>$$
>1001|0111|1010 = 9 + 7 + 10 =26
>$$
>
>Adesso dividiamo questo risultato per il numero di bucket e prendiamo il resto della divisione, questo sarà il bucket. Ad esempio se $B=3$ allora calcoliamo $26\%3=2$, quindi il record che ha questa chiave andrà inserito nell’ultimo blocco del bucket 2.

>[!warning] Chiave
>Quando ci rifermiamo a chiave di hash non intendiamo sempre la chiave relazionale dell'attributo. La chiave di hash può anche essere un insieme di attributi su cui facciamo spesso operazioni.

---
## Operazioni

Una qualsiasi operazione in un file hash richiede:

- Valutazione della funzione di hash per _v_, `h(v)`, per individuare il bucket, per noi questo ha costo 0 dato che ci interessano soltanto gli accessi in memoria.
- Esecuzione dell’operazione sul bucket che è organizzato come un heap.

Inoltre dato che l’inserimento di nuovi record viene effettuato sull’ultimo bucket, la bucket directory dovrà contenere anche un puntatore all’ultimo record di ogni bucket oltre che al loro inizio.

Quindi se la funzione di hash distribuisce in modo uniforme i record nei vari bucket avremo che ogni bucket è costituito da Bn​ blocchi e quindi il costo richiesto da un’operazione è approssimativamente $\frac{1}{b} - \text{esimo}$ del costo della stessa operazione eseguita su un file heap.

---
## Osservazione

Ovviamente più bucket abbiamo più è basso il costo delle operazioni, ma dobbiamo fare delle considerazioni che ci portano a limitare questo numero:
- Ogni bucket deve avere almeno un blocco
- La bucket directory deve avere una dimensione tale da essere mantenuta in memoria principale altrimenti effettueremo accessi per leggere i blocchi della bucket directory.