---
type: Uni Note
class:
  - "[[Basi di Dati 1 (class)]]"
academic year: 2024/2025
related: "[[Algebra Relazionale]]"
completed: false
created: 2024-10-15T18:30
updated: 2024-10-17T18:25
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
>$$

>[!warning] Negazione dell'operatore universale
>
>La negazione di “per ogni” **non è** “per nessuno” ma:
> $$
>\text{“esiste almeno un elemento per cui la condizione è falsa”}
>$$
>
>>**Ovvero:** La negazione di **TUTTI** non è **NESSUN** ma **NON TUTTI** (almeno uno)

---
## Risoluzione di Query con Operatore Universale 

Risolvere delle query con operatore universale può essere meno intuitivo rispetto a risolvere query con operatore universale.

Infatti prima di poter scegliere se inserire o no una tupla nel risultato dobbiamo valutare tutte le altre tuple.

Il problema è che non esiste un operatore che prima di inserire una tupla nel risultato controlla tutte quelli precedenti.

>[!done] Soluzione
>Visto che non c'è un operazione immediato dobbiamo risolvere il problema in più passaggi
>
>1. Eseguiamo la query con la condizione negata
>2. Troviamo gli oggetti che ALMENO una volta soddisfano la condizione CONTRARIA 
>3. Eliminiamo gli oggetti ottenuti nel passaggio 2 dalla risposta con l’operatore di differenza

>[!example]- Esempio Dettagliato
>**Query:** Nomi e città dei clienti che hanno SEMPRE ordinato più di 100 pezzi per un articolo
>
>**Relazioni:**
>>[!column|flex]
>>
>>>[!NOTE|clean no-icon] Ciente
>>>
>>>| Nome | C# | Città |
>>>| --- | --- | --- |
>>>| Rossi | C1 | Roma |
>>>| Rossi | C2 | Milano |
>>>| Bianchi | C3 | Roma |
>>>| Verdi | C4 | Roma |
>>
>>>[!NOTE|clean no-icon] Ordine
>>>
>>>| C# | A# | N-pezzi |
>>>| --- | --- | --- |
>>>| C1 | A1 | 100 |
>>>| C2 | A2 | 200 |
>>>| C3 | A2 | 150 |
>>>| C4 | A3 | 200 |
>>>| C1 | A2 | 200 |
>>>| C1 | A3 | 100 |
>
>**Effettuiamo un join tra le due relazioni:** $\text{Cliente} \bowtie \text{Ordine}$
>
>| Nome | C# | Città | A# | N-pezzi |
>| --- | --- | --- | --- | --- |
>| Rossi | C1 | Roma | A1 | 100 |
>| Rossi | C1 | Roma | A2 | 200 |
>| Rossi | C1 | Roma | A3 | 100 |
>| Rossi | C2 | Milano | A2 | 200 |
>| Bianchi | C3 | Roma | A2 | 150 |
>| Verdi | C4 | Roma | A3 | 200 |
>
>Ora dobbiamo ottenere tutte le tuple della relazione $\text{Cliente} \bowtie \text{Ordine}$  che non rispettano la **Query**, in questo caso dobbiamo trovare tutti i clienti che hanno fatto un ordine non superiore a 100 pezzi.
>
>$$
>\sigma_{\text{N-pezzi}\leq 100}(\text{Cliente} \bowtie \text{Ordine})
>$$
>
>| Nome | C# | Città | A# | N-pezzi |
>| --- | --- | --- | --- | --- |
>| Rossi | C1 | Roma | A1 | 100 |
>| Rossi | C1 | Roma | A3 | 100 |
>
>
>Ora otteniamo nome e città dei clienti che non hanno clienti che hanno fatto un ordine non superiore a 100 pezzi, facendo una proiezione dei campi Nome, Città sul risultato del passaggio precedente.
>
>$$
>\pi_{\text{Nome, Città}} \big(\sigma_{\text{N-pezzi}\leq 100}(\text{Cliente} \bowtie \text{Ordine})\big)
>$$
>
>| Nome | Città | 
>| --- | --- | 
>| Rossi | Roma |
>
>Infine, per ottenere i nomi e le città dei clienti che hanno SEMPRE ordinato più di 100 pezzi per un articolo, dobbiamo escludere i clienti che hanno fatto un ordine non superiore a 100 pezzi. Possiamo fare questo utilizzando l'operazione di differenza.
>
>$$
>\pi_{\text{Nome, Città}}(\text{Cliente} \bowtie \text{Ordine}) - \pi_{\text{Nome, Città}} \big(\sigma_{\text{N-pezzi}\leq 100}(\text{Cliente} \bowtie \text{Ordine})\big)
>$$
>
>| Nome | Città |
>| --- | --- |
>| Rossi | Milano |
>| Bianchi | Roma |
>| Verdi | Roma |

>[!example]- Esempio Breve
>**Query:** Nomi e città dei clienti che non hanno MAI ordinato più di 100 pezzi per un articolo
>
>**Relazioni:**
>>[!column|flex]
>>
>>>[!NOTE|clean no-icon] Ciente
>>>
>>>| Nome | C# | Città |
>>>| --- | --- | --- |
>>>| Rossi | C1 | Roma |
>>>| Rossi | C2 | Milano |
>>>| Bianchi | C3 | Roma |
>>>| Verdi | C4 | Roma |
>>
>>>[!NOTE|clean no-icon] Ordine
>>>
>>>| C# | A# | N-pezzi |
>>>| --- | --- | --- |
>>>| C1 | A1 | 100 |
>>>| C2 | A2 | 200 |
>>>| C3 | A2 | 150 |
>>>| C4 | A3 | 200 |
>>>| C1 | A2 | 200 |
>>>| C1 | A3 | 100 |
>
>Seguendo lo stesso ragionamento dell'esempio precedente, troviamo prima chi non rispetta la query:
>
>$$
>\pi_{\text{Nome, Città}} \big(\sigma_{\text{N-pezzi}> 100}(\text{Cliente} \bowtie \text{Ordine})\big)
>$$
>
>Poi effettuiamo la differenza:
>
>$$
>\pi_{\text{Nome, Città}}(\text{Cliente} \bowtie \text{Ordine}) - \pi_{\text{Nome, Città}} \big(\sigma_{\text{N-pezzi}> 100}(\text{Cliente} \bowtie \text{Ordine})\big)
>$$
>
>La query in questo caso restituisce un risultato vuoto.
