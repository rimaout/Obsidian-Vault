---
type: Uni Note
class:
  - "[[Basi di Dati 1 (class)]]"
academic year: 2024/2025
related: 
completed: false
created: 2024-11-13T14:33
updated: 2024-11-14T12:26
---
>[!abstract] Related
>- 

---
## Introduzione

Dati uno schema di relazione $R$ e un insieme di dipendenze funzionali $F$ su $R$, $R$ è in **3NF** se:

$$
\forall X \to  A \in F^{+} , A \not \in X
$$



## Dipendenze Parziali e Transitive



>[!note] Definizione 3NF
>
>Un schema di relazione $R$  è in terza forma normale (3NF) se:
>
>$$
>\forall X \rightarrow A \in F^+, A \notin X
>$$
>
>* $A$  appartiene ad una chiave (è primo) 
>
>Oppure
>
>* $X$  contiene una chiave (è una superchiave)


>[!warning] Nota importante
>
>Non è sufficiente considerare solo le dipendenze funzionali in $F$ , poiché non possiamo gestire le dipendenze con più attributi a destra. Invece, dobbiamo considerare le dipendenze funzionali in $F^{+}$, che includono anche le dipendenze derivate.

>[!example] Esempio
>
>Se abbiamo una dipendenza funzionale $X \rightarrow AB$, possiamo scomporla in due dipendenze funzionali $X \rightarrow A$ e $X \rightarrow B$. Quindi, dobbiamo considerare le dipendenze funzionali in $F^{+}$  per garantire che la condizione di 3NF sia soddisfatta.
x
Condizione equivalente
La condizione di 3NF può essere scritta anche come:

$$\forall X \rightarrow Y \in F^+, \forall A \in Y, A \text{ è primo o } X \text{ contiene una chiave}$$

Questa condizione garantisce che ogni attributo non primo dipenda solo da una chiave o da una super-chiave.

>[!warning] Importanza della 3NF
>
>La terza forma normale è importante perché aiuta a ridurre la ridondanza dei dati e a migliorare la coerenza dei dati. Inoltre, essa facilita la gestione e la manutenzione dei dati, poiché riduce il numero di modifiche che devono essere apportate in caso di aggiornamenti o cancellazioni di dati.

