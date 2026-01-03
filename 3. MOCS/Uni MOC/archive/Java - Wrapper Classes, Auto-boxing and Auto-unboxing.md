---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: true
created: 2025-01-29T21:15
updated: 2025-01-30T15:46
---
### Classi Wrapper

Sono classi "involucro" che permettono di convertire in oggetti i valori dei tipi primitivi, fornendo metodi e funzionalità aggiuntive.

>[!warning] Utilizzi
>
>Necessario quando si lavora con strutture dati come le [[Java - Collections|collezioni]], che accettano solo oggetti e non tipi primitivi.
>
>Aggiungono metodi per la manipolazione dei primitivi:
>- `compareTo()`
>- `valueOf()`
>- conversioni tra tipi (es. `Integer.parseInt("20")`)

### Auto-Boxing

L'auto-boxing è il processo di conversione automatica di un ***tipo primitivo*** in un ***oggetto wrapper*** corrispondente. 

Ad esempio, se si ha un valore di tipo `int` e si vuole assegnarlo a un oggetto di tipo `Integer`, Java eseguirà automaticamente la conversione.

```java
int x = 10;
Integer y = x; // auto-boxing: int -> Integer
```

### Auto-Unboxing

L'auto-unboxing è il processo di conversione automatica di un oggetto wrapper in un tipo primitivo corrispondente. 

Ad esempio, se si ha un oggetto di tipo `Integer` e si vuole assegnarlo a una variabile di tipo `int`, Java eseguirà automaticamente la conversione.

```java
Integer x = 10;
int y = x; // auto-unboxing: Integer -> int
```
