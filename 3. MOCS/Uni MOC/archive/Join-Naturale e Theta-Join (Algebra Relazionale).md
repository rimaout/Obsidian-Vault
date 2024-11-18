---
type: Uni Note
class:
  - "[[Basi di Dati 1 (class)]]"
academic year: 2024/2025
related:
  - "[[Algebra Relazionale]]"
completed: false
created: 2024-10-09T16:48
updated: 2024-11-16T12:20
---
>[!abstract] Related
>- [[Operatori (Algebra Relazionale)]]
>- [[Algebra Relazionale]]
>- [[Basi di Dati 1 (class)]]

---
## Join Naturale

>[!note] Definizione
>Il join naturale è un'operazione che combina due relazioni in base a una o più colonne comuni.
>
>$$
>r_{1} \bowtie r_{2}
>$$
>
>>**Condizione:** Le colonne comuni devono avere lo stesso nome e tipo di dati.

>[!example]- Esempio
>
>>[!column|flex]
>>
>>>[!warning| clean no-icon] Relazione Ordini
>>>
>>>| ID_ordine | ID_cliente | Data_ordine |
>>>| --- | --- | --- |
>>>| 1 | 1 | 2022-01-01 |
>>>| 2 | 2 | 2022-01-15 |
>>>| 3 | 1 | 2022-02-01 |
>>
>>>[!warning| clean no-icon] Relazione Clienti
>>>
>>>| ID_cliente | Nome | Indirizzo |
>>>| --- | --- | --- |
>>>| 1 | Mario Rossi | Via Roma 1 |
>>>| 2 | Luca Verdi | Via Milano 2 |
>
>>[!todo] Join Naturale
>>
>>$$
>>\text{Ordini} \bowtie \text{Clienti}
>>$$
>>
>>| ID_ordine | ID_cliente | Data_ordine | Nome | Indirizzo |
>>| --- | --- | --- | --- | --- |
>>| 1 | 1 | 2022-01-01 | Mario Rossi | Via Roma 1 |
>>| 3 | 1 | 2022-02-01 | Mario Rossi | Via Roma 1 |
>>| 2 | 2 | 2022-01-15 | Luca Verdi | Via Milano 2 |

---
## Theta Join

>[!note] Definizione
>Il theta join è un'operazione che combina due relazioni in base a una condizione di join arbitraria.
>
>$$
>r_{1} \bowtie_{\theta} r_{2}
>$$
>
>>**Condizione:** Con $\theta$ si intende la condizione di join ovvero può una qualsiasi espressione booleana che coinvolga attributi delle due relazioni.
>
> >**Osservazione** 
>Nel caso in cui la condizione di join sia una semplice uguaglianza tra attributi, il theta join coincide con il [[#Join Naturale]].

>[!example]- Esempio
>
>>[!column|flex]
>>
>>>[!warning| clean no-icon] Relazione Ordini
>>>
>>>| ID_ordine | ID_cliente | Data_ordine |
>>>| --- | --- | --- |
>>>| 1 | 1 | 2022-01-01 |
>>>| 2 | 2 | 2022-01-15 |
>>>| 3 | 1 | 2022-02-01 |
>>
>>>[!warning| clean no-icon] Relazione Clienti
>>>
>>>| ID_cliente | Nome | Indirizzo |
>>>| --- | --- | --- |
>>>| 1 | Mario Rossi | Via Roma 1 |
>>>| 2 | Luca Verdi | Via Milano 2 |
>
>>[!todo] Theta Join
>>
>>$$
>>\text{Ordini} \bowtie_{ID\_cliente = ID\_cliente} \text{Clienti}
>>$$
>>
>>| ID_ordine | ID_cliente | Data_ordine | Nome | Indirizzo |
>>| --- | --- | --- | --- | --- |
>>| 1 | 1 | 2022-01-01 | Mario Rossi | Via Roma 1 |
>>| 3 | 1 | 2022-02-01 | Mario Rossi | Via Roma 1 |
>>| 2 | 2 | 2022-01-15 | Luca Verdi | Via Milano 2 |

>[!example]- Esempio con condizione di join diversa
>
>>[!column|flex]
>>
>>>[!warning|clean no-icon] Relazione Ordini
>>>
>>>| ID_ordine | ID_cliente | Data_ordine |
>>>| --- | --- | --- |
>>>| 1 | 1 | 2022-01-01 |
>>>| 2 | 2 | 2022-01-15 |
>>>| 3 | 1 | 2022-02-01 |
>>
>>>[!warning|clean no-icon] Relazione Clienti
>>>
>>>| ID_cliente | Nome | Indirizzo |
>>>| --- | --- | --- |
>>>| 1 | Mario Rossi | Via Roma 1 |
>>>| 2 | Luca Verdi | Via Milano 2 |
>
>>[!todo] Theta Join con condizione di join diversa
>>
>>$$
>>\text{Ordini} \bowtie_{ID\_cliente > 1} \text{Clienti}
>>$$
>>
>>| ID_ordine | ID_cliente | Data_ordine | Nome | Indirizzo |
>>| --- | --- | --- | --- | --- |
>>| 2 | 2 | 2022-01-15 | Luca Verdi | Via Milano 2 |
