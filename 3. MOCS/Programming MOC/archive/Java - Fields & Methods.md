---
created: 2024-03-08
type: Programming Note
programming language: "[[Java MOC]]"
related:
  - "[[Metodologie di Programmazione (class)]]"
completed: true
updated: 2025-02-07T10:38
---
## Campi

Un campi (detto anche *variabile di istanza*) costituiscono la **memoria privata** di un oggetto, e non sono altro che variabili che quindi hanno un nome ed un tipo di dati.

>[!note] Dichiarazione di un campo
>
>`private [static] [final] tipo_di_dati nome`
>- [[Java - Access Modifier|private]]: tipicamente ad accesso privato
>- [[Java - Static|static]]: indica che il campo è condiviso da tutti gli oggetti 
>- [[Java - Final|final]]:indica che il campo è una cotante (il valore non può essere modificato una volta dichiarato) 
>
>
>***oss:*** le parentesi quadre indicano l’opzionalità del parametro

>[!note] Inizializzazione Implicita
>
>Al momento della creazione dell’oggetto i campi di una classe sono inizializzati automaticamente
>
>
>| Tipo del campo    | Valore di Inizializzazione |
>| ----------------- | ------------------------------ |
>| `int`, `long`     | `0`, `0L`                      |
>| `float`, `double` | `0.0f`, `0.0`                  |
>| `char`            | `'\0'`                         |
>| `boolean`         | `false`                        |
>| `classe X`        | `null`                         |
> 
>>**oss:** L'inizializzazione è automatica solo per i campi di classe, ma NON per le variabili locali dei metodi

>[!note] Campi vs Variabili Locali
>| Campi | Variabili |
>| -------- | -------- |
>| I campi sono variabili dell'oggetto. | Le variabili locali sono variabili definite all'interno di un metodo. |
>| Sono variabili almeno all'interno di tutti gli oggetti della stessa classe, e esistono per tutta la vita di un oggetto. | Sono definite come parametri del metodo, o all'interno del corpo del metodo, ed esistono dal momento in cui sono definite fino al termine dell'esecuzione della chiamata al metodo in questione. |

---
## Metodi

Un metodo è un blocco di codice che esegue una specifica azione o calcolo. In particolare sono utilizzati per interagire con un oggetto (interfaccia publica) o o per effettuare calcoli interni (metodi privati).

>[!note] Dichiarazione di un metodo
>
>`[public/private/protected] [static] [final] tipo_di_ritorno nome(parametri)`
>- [[Java - Access Modifier|public, private, protected]]: accesso al metodo
>- [[Java - Static|static]]: indica che il metodo è condiviso da tutti gli oggetti
>- [[Java - Final|final]]: indica che il metodo non può essere sovrascritto
>- `tipo_di_ritorno`: tipo di valore restituito dal metodo
>- `nome`: nome del metodo
>- `parametri`: lista di parametri passati al metodo
>
>***oss:*** le parentesi quadre indicano l'opzionalità del parametro

>[!danger] Overloading & Numero Variabile di Parametri
>
>***Overloading:*** [[Java - Overloading & Overriding]]
>
>***Numero Variabile di Parametri:*** è possibile creare metodi che accettano un numero nn specificato di parametri, ma tutti dello stesso tipo:
>
>```java
>public double sum(double ... valori){  
>    double somma = 0;  
>    for (double v : valori) {  
>        somma *= v;  
>    }  
>    return somma;  
>}
>```
>
>I parametri vengono trasformati in una lista
