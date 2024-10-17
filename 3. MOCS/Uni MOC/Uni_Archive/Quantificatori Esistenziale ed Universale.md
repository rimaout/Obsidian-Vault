---
type: Uni Note
class:
  - "[[Basi di Dati 1 (class)]]"
academic year: 2024/2025
related: "[[Algebra Relazionale]]"
completed: false
created: 2024-10-15T18:30
updated: 2024-10-15T19:11
---
>[!abstract] Index
>1. [[#Quantificatore Esistenziale]]
>2. [[#Quantificatore Universale]]

>[!abstract] Related
>- [[Algebra Relazionale]]

---
## Quantificatore Esistenziale

Fino ad ora abbiamo utilizzato query che implicavano l'utilizzo di condizioni equivalenti al quantificatore esistenziale.

$$
\exists\ \ \text{(esiste almeno un)}
$$

Questo tipo di interrogazioni sono facili da rispondere, basta controllare in modo sequenziale (una tupla alla volta) se la tupla verifica o meno la condizione.

Quando si incontra una tuple che soddisfa le condizioni, questa viene inserita nel risultato

>[!example] Esempio
>
>Un esempio di query che utilizza il quantificatore esistenziale è:
>
>$$
>\text{Query: Codici dei clienti che hanno effettuato \textcolor{red}{almeno} un ordine per più di 100 pezzi}
>$$

---
## Quantificatore Universale

Le condizioni delle query possono anche richiedere la valutazione di gruppi interi di tuple prima di decidere se inserirerle o meno nel risultato.

>**oss:** Le tuple una volta inserite in un risultato non possono essere rimosse.

In questo caso la condizione equivale a valutare il quantificatore universale:

$$
\begin{align*}
& - \ \ \ \forall \ \ \ \text{(per ogni)} \\
& - \ \ \ ! \exists \ \ \text{(non esiste nessun)}
\end{align*}
$$

>[!example] Esempio
>Un esempio di query che utilizza il quantificatore universale è:
>
>$$
>\text{Query: Codice dei clienti che hanno \textcolor{red}{sempre} ordinato più di 100 pezzi per un articolo}
$$
