---
type: Uni Note
class:
  - "[[Algoritmi 2 (class)]]"
academic year: 2024/2025
related: 
completed: true
created: 2025-03-05T08:36
updated: 2025-03-10T19:29
---
## Grafo

Grafo definito da $G(V,E)$, dove:
- $V$ è l'insieme dei *vertici*
- $E$ è l'insieme degli *archi*

E definiamo $n = |V|$ e $m = |E|$.

>[!warning] Grado di un nodo
>
>Il grado di un nodo è il numero di archi di cui fa parte.
>
>Se il grafo è diretto allora esiste anche il grado entrante ed il grado uscente:
>- *Grado entrante:* numero di archi ....
>- *Grado uscente:* numero di archi ....

## Tipi di Grafi

>[!note] Grafo Diretto
>
>Un grafo si dice **diretto** quando i gli archi hanno una direzione.
>
>$$
>\begin{align*}
>& - \ \ \ 0 \leq m \leq n(n-1) = O(n^{2})\ \ \text{se il grafo è diretto}\\
>& - \ \ \ 0 \leq m \leq \frac{{n(n-1)}}{2} = O(n^{2})\ \ \text{se il grafo non è diretto}
>\end{align*}
>$$
>
>---
>
>Un **pozzo** è un *nodo senza archi uscenti*, un pozzo si dice **universale** se tutti gli altri nodi del grafo hanno un arco uscente verso il pozzo, esiste un solo pozzo universale.
>
>Una **sorgente** è un *nodo con soli archi uscenti*.

^e35772

>[!note] Grafo Sparso o Denso
>
>Un grafo si dice **sparso** se $m = O(n)$.
>
>Un grafo si dice **denso** se $m = \Omega(n^{2})$.
>
>>***oss:*** esistono grafi che non sono ne densi ne sparsi, es. $m = \Theta(n \log n)$.

>[!note] Grafo Completo
>
>Un grafo si dice **completo** se se ha tutto gli archi possibili, ovvero $m = \Theta(n^{2})$.

>[!note] Grafo Connesso
>
>Un grafo **connesso** è un grafo in cui *esiste un percorso tra ogni coppia di vertici*. In altre parole, è possibile raggiungere ogni vertice da ogni altro vertice attraverso una sequenza di archi.

>[!note] Torneo
>
>Un grafo si si dice **torneo** se tra ogni coppia di nodi c'è esattamente un arco, ovvero $m = \Theta(n^{2})$.

>[!note] Grafo Planare
>
>Un grafo si dice **planare** se è possibile disegnarlo sul piano senza che gli archi si intersechino.
>
>![[Pasted image 20250228170204.png|700]]
>
>>[!danger] Teorema di Eulero
>>
>>Un grafo planare di $n>2$ nodi ha al più $3n−6$ archi
>>
>>![[Pasted image 20250302124401.png|700]]
>>
>>- La *prima colonna* della tabella ci mostra il numero `m` di archi di un grafo completo di `n` nodi, ovvero il numero `m` massimo di archi.
>>- La *seconda colonna* ci mostra il numero `m` di archi fino a cui un grafo di `n` nodi ha la possibilità di essere planare.
>>
>>Quindi ad esempio un grafo da `6` nodi e `13` archi è sicuramente non planare, ma con `12` archi potrebbe essere planare.

>[!note] Albero
>
>Un **albero** è un *grafo sparso* connesso senza cicli.
>
>![[Pasted image 20250228163658.png|550]]
>
>>[!danger] Info
>> 
>>- I nodi di *grado 1* in un albero vengono chiamati **foglie**.  
>>- In un albero di `n` nodi ci saranno esattamente `m = n-1` archi (per questo un albero è sempre sparso).
>>- Se rimuoviamo una foglia rimane comunque un albero.
>>- Tutti li alberi sono grafi planari, ma non tutti i grafi planari sono alberi.
