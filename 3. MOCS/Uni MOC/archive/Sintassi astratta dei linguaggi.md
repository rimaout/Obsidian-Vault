---
type: Uni Note
class:
  - "[[Linguaggi di Programmazione (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-10-27T11:25
updated: 2025-10-27T14:08
---
Appunti rubati da [@exiss](https://github.com/Exyss/university-notes)

>[!note] Definizione: Linguaggio
>
>Definiamo come linguaggio un *insieme di stringhe*

>[!note] Definizione: Grammatica
>
>Definiamo come grammatica un *insieme di regole*, dette **termini**, che definiscono come poter manipolare le stringhe di un linguaggio.
>
>La forma di ***Backus-Naur*** è una notazione utilizzata per descrivere grammatiche ed è definita come:
>
>$$
><\text{symbol}>\, ::=\, \, \_\text{expression}\_
>$$
>
>Dove:
>- `<symbol>` è un simbolo non-terminale espresso dalla grammatica
>- L'operatore `::=` indica che ciò che si trova alla sua sinistra può essere sostituito con ciò che si trova alla sua destra
>- `<_expression_>` consiste in una o più sequenze di simboli terminali o non-terminali, dove ogni sequenza è separata da una barra verticale (ossia `|`) indicante una scelta possibile per l’operatore `::=`.
>
>>[!example] Esempio
>>
>>Consideriamo il linguaggio $L$ espresso dalla grammatica:
>>
>>$$
>>M,N\ ::=\ 0 \mid 1 \mid \dots \mid M+N \mid M \cdot N
>>$$
>>
>>Tale grammatica indica che i simboli non-terminali `M` e `N` possono essere sostituiti con:
>>- un numero naturale
>>- un’espressione $M+N$ o $M\cdot N$ dove `M` e `N` sono due ulteriori simboli terminali o non-terminali
>>
>>Ad esempio, la stringa `5 + 7` è ben definita dalla grammatica, mentre la stringa `5 + +` non lo è

>[!note] Definizione: Sintassi Astratta
>
>La sintassi astratta di un linguaggio è una definizione induttiva di un insieme `T` di *termini*, che permettendo di definire strutture algebriche senza dover necessariamente definire concretamente le sue operazioni.
>
>>[!example] Esempio
>>
>>Consideriamo ancora il linguaggio $L$ definito dalla grammatica:
>>
>>$$
>>M,N\, ::=\, 0 \mid 1 \mid \dots \mid M+N \mid M \cdot N
>>$$
>>
>>Definiamo quindi la funzione $eval: L \to \mathbb{N}$ in grado di valutare le espressioni del linguaggio:
>>
>>$$
>>\begin{align*}
>>&\text{eval}(x0\text{"}) = 0\\
>>&\text{eval}(\text{``}1\text{''}) = 1\\
>>&\dots\\
>>&\text{eval}(\text{"}M+N\text{"}) = \text{eval}(\text{"}M\text{"}) + \text{eval}(\text{"}N\text{"})\\
>>&\text{eval}(\text{"}M\cdot N\text{"}) = \text{eval}(\text{"}M\text{"}) \cdot  \text{eval}(\text{"}N\text{"})
>>\end{align*}
>>$$
>>
>>Notiamo quindi che la grammatica definisce in modo astratto (ma concretamente tramite eval) le seguenti operazioni:
>>
>>$$
>>\begin{align*}
>>&0:\ \mathbb{1} \to \mathbb{N}: () \to  0\\
>>&1:\ \mathbb{1} \to \mathbb{N}: () \to  1\\
>>&\dots\\
>>&\text{plus:}\ \ \; \mathbb{N} \times \mathbb{N} \to \mathbb{N}: (m,n) \mapsto  m+n\\
>>&\text{times:}\ \mathbb{N} \times \mathbb{N} \to \mathbb{N}: (m,n) \mapsto  m\cdot n
>>\end{align*}
>>$$
>>
>>>***Nota:*** le operazioni `plus` e `times` non sono né iniettive né con immagini disgiunte. Di conseguenza, la funzione `eval` non ci permette di definire un’algebra induttiva.
>>>
>>>Tuttavia, per tale linguaggio è comunque possibile definire (in qualche modo, ad esempio fissando una precedenza per le operazioni rompendo proprietà come l’associatività e la commutatività) una funzione che possa descrivere un’algebra induttiva.

^83963b

>[!danger] Teorema: Algebra induttiva dei termini
>
>Dato un linguaggio con una [[#^83963b|sintassi astratta]] con termini definiti in `T`, esiste sempre un’algebra induttiva $(T,\alpha)$. Di conseguenza, tutte le proprietà di un linguaggio sono dimostrabili tramite l’induzione strutturale sulla sua algebra dei termini.
>
>(dimostrazione omessa)
