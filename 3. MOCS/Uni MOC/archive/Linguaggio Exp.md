---
type: Uni Note
class:
  - "[[Linguaggi di Programmazione (class)]]"
academic year: 2024/2025
related:
completed: false
created: 2025-10-27T13:59
updated: 2025-11-12T18:08
---
## Introduzione Linguaggi Funzionali

 Introduciamo un semplice linguaggio di espressioni aritmetiche `Exp` composto dall'apparato linguistico minimo per poter studiare la nozione di variabile di un linguaggio di programmazione funzionale (esempio SML, Haskell e LISP). 
 
 Arricchendo questo linguaggio con la nozione di funzione (ovvero l’astrazione di un termine rispetto ad una variabile) otterremo poi un linguaggio estremamente espressivo, [[Linguaggio Fun|Fun]] dove impareremo a codificare booleani, liste, numeri e gran parte dell’aritmetica.

`Exp` e `Fun` ci permetteranno di mettere a confronto:
- il binding **statico** e quello **dinamico**.
- le strategie di valutazione **eager** e quella **lazy**.

|           | **statico** | **dinamico** |
| --------- | ----------- | ------------ |
| **eager** | SML         | Emacs Lisp   |
| **lazy**  | Haskell     | S-Plus       |

## Definizione Exp

>[!note] Definizione: Linguaggio Exp
>
>Definiamo come `Exp` il linguaggio rappresentato dalla seguente grammatica:
>
>$$
>M,N\ ::=\ k \mid x \mid M + N \mid \text{let } x = M \text{ in } N
>$$  
>
>Dove:
>- $k \in \{0,1,\dots\}$ ossia è una ***cotante***
>- $x \in Var = \{ x,y,z,\dots \}$ ossia è una ***variabile***
>- $+:\ \text{Var} \times \text{Exp} \times \text{Exp} \to \text{Exp}$ la quale *assegna* alla variabile $x$ l'espressione $M$ all'interno della *valutazione* di $N$. Inoltre, $x$ prende il nome di variabile locale all'interno di $N$.
>- $Val = \{ 0,1,\dots \}$ è l’insieme

>[!example] Esempi
>
>- L'espressione $let\ x=3 \text{ in } x+1$ indica che la variabile $x$ assume valore 3 all'interno della valutazione $x+1$. Di conseguenza il risultato della valutazione è 4
>- L'espressione $let\ x = 3 \text{ in } 7$ è valutata come 7
>- L'espressione $let\ y = 9 \text{ in } (let\ x = (let\ y = 2 \text{ in } y+1) \text{ in } x+y)$ viene valutata come 12

>[!note] Definizione: Scope di una variabile
>
>Data un'espressione e una variabile $x$, definiamo come scope di $x$ la *porzione dell’espressione* all'interno della quale una *variabile può essere riferita*, ossia per cui ne è definito il valore.

>[!note] Definizione: Variabile Libera
>
>Data un’espressione `expr`, definiamo $x \in expr$ come variabile libera se `x` non ha un valore assegnato durate la valutazione di `expr`.
>
>>[!example] Esempio
>>
>>L'espressione $let\ x = (let\ y = 2 \text{ in } y+1) \text{ in } x+y$ non è coerente con la grammatica di `Exp`, poiché `y` non definito durante la valutazione di $x+y$. 
>>
>>Di conseguenza, non è possibile valutare l'espressione.

## Ambienti

Un ambiente è una funzione parziale (ossia non necessariamente definita su tutto il dominio) che associano ogni variabile al proprio valore:
$$
Env = Var \overset{fin}{\to} Val
$$



