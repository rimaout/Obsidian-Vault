---
Created: 2024-03-08
Type: Programming Note
Programming Language: "[[Java MOC]]"
Related:
  - "[[Java OOP]]"
Completed: false
---
---

>[!info] Index
>1. [[#Introduzione]]
>2. [[#Dichiarazione di un campo]]
>3. [[#Inizializzazione implicita]]
>4. [[#Campi vs. variabili locali]]

---

### Introduzione 

>[!note] Definizione
>Un campo (detto anche variabile di istanza) costituisce la memoria privata di un oggetto
>- Ogni campo ha un tipo di dati (es. il valore del contatore è intero)
>- Ogni campo ha un nome fornito dal programmatore (es. value nella diapositiva precedente)

---
## Dichiarazione di un campo

>[!tip] Dichiarazione
>`private [static] [final] tipo_di_dati nome`
>- `private`: tipicamente ad accesso privato
>- `static`: indica che il campo è condiviso da tutti gli oggetti 
>- `final`:indica che il campo è una cotante (il valore non può essere modificato una volta dichiarato) 
>
>*oss:* le parentesi quadre indicano l’opzionalità del parametro

---
## Inizializzazione implicita
Al momento della creazione dell’oggetto i campi di una classe sono inizializzati automaticamente

| Tipo del campo    | Inizializzato implicitamente a |
| ----------------- | ------------------------------ |
| `int`, `long`     | `0`, `0L`                      |
| `float`, `double` | `0.0f`, `0.0`                  |
| `char`            | `'\0'`                         |
| `boolean`         | `false`                        |
| `classe X`        | `null`                         |
> [!warning]
> le inizializzazioni sono automatiche per i campi di classe, ma NON per le variabili locali dei metodi

---
## Campi vs. variabili locali

| Campi                                                                                                                  | Variabili locali                                                                                                                                                                |
| ---------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| I campi sono variabili dell’oggetto                                                                                    | Le variabili locali sono variabili definite all’interno di un metodo                                                                                                            |
| sono variabili almeno all’interno di tutti gli oggetti della stessa classe ed esistono per tutta la vita di un oggetto | come parametri del metodo o all’interno del corpo del metodo ed esistono dal momento in cui sono definite fino al termine dell’esecuzione della chiamata al metodo in questione |

---