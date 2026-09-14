---
type: Uni Note
class:
  - "[[TPFI]]"
academic year: 2024/2025
related:
completed: true
created: 2026-06-07T13:30
updated: 2026-07-14T12:07
---
## Introduzione

Le funzioni sono visti come moduli elementari che possono essere combinati tra loro per costruire operazioni più complesse in modo elegante e matematicamente rigoroso.

## Teoria e Regole di Tipaggio

Dal punto di vista matematico, la composizione di due funzioni $f$ e $g$ si scrive $f \circ g$. In Haskell, questo concetto è implementato dall'operatore infisso `(.)`.

```haskell
(f . g) x = f (g x)
```

Questo significa che il risultato della funzione $g$ (applicata all'argomento $x$) diventa l'input per la funzione $f$.

>[!note] Il Politipo della Composizione
>
>L'operatore `.` è una funzione di **ordine superiore** perché accetta altre funzioni come argomenti. Il suo tipo è:
>
>```
>(.) :: (b -> c) -> (a -> b) -> a -> c
>```
>
>- **`(b -> c)`**: La prima funzione ($f$) che prende un valore di tipo $b$ e restituisce un tipo $c$.
>- **`(a -> b)`**: La seconda funzione ($g$) che prende un valore di tipo $a$ e restituisce un tipo $b$.
>- **`a -> c`**: Il risultato è una nuova funzione che trasforma direttamente un input $a$ in un output $c$.

>[!note] La Eta-Regola (Point-free Style)
>
>La teoria permette di omettere i parametri se essi compaiono allo stesso modo a destra e a sinistra di un'equazione. Questa è nota come **eta-regola**. Grazie ad essa, possiamo scrivere definizioni in "point-free style", concentrandoci sulla combinazione dei blocchi logici piuttosto che sulla manipolazione esplicita dei dati.
>
>Ad esempio Ila funzione `any` può essere definita in diversi modi:
>
>1. Versione estesa: `myAny p xs = or (map p xs)`
>2. Uso della composizione: `myAny p xs = (or . map p) xs`
>3. Applicazione della **eta-regola**: siccome `xs` è l'ultimo argomento di entrambi i lati, lo cancelliamo ottenendo `myAny p = or . map p`.
>   
>>***Nota:*** in questo caso la versione con l'eta regola può essere utilizzata soltanto con l’utlilizzo della composizione di funzione.

>[!note] Ragionamento Equazionale
>
>La composizione è fondamentale per provare la correttezza dei programmi. Un'equazione celebre è: `map (f . g) = (map f) . (map g)`. Questa legge afferma che mappare una funzione composta su una lista è equivalente a mappare la prima funzione sul risultato della mappatura della seconda.

## Utilizzi ed Esempi Pratici

>[!note] Grandi Composizioni
>
>La scrittura `(f1 . f2 . f3) x` è equivalente a `f1 (f2 (f3 x))` ed è un modo pulito per evitare troppe parentesi annidate.

>[!note] Trasformazioni Semplici
>
>Possiamo comporre funzioni standard per manipolare liste in un colpo solo:
>
>```haskell
>map ((*2) . length) ["I", "love", "haskell"]
>```
>
>Qui, per ogni stringa, viene prima calcolata la `length` (es. 7) e poi applicato il raddoppio `(*2)`, ottenendo `14`.

>[!note] Definizione di Predicati (`any` e `all`)
>
>Le funzioni `any` (esiste un elemento che...) e `all` (tutti gli elementi...) sono definite componendo `map` con i riduttori booleani `or` e `and`:
>
>- `myAny p = or . map p`
>- `myAll p = and . map p`.


