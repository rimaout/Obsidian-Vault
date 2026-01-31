---
type: Uni Note
class:
  - "[[Basi di Dati 2 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-03-04T16:02
updated: 2026-01-31T13:32
---
## Introduzione

Durante l'analisi concettuale dobbiamo definire il tipo di ogni attributo, di classe e di associazione.

>[!note] Tipi di dati concettuali
>
>Dunque, vogliamo utilizzare **tipi di dato concettuali**, che siano facilmente realizzabili con qualsivoglia tecnologia informatica (Python, Java, sistemi di gestione di basi di dati, etc.)
>
>***Tipi base:*** Intero, Reale, Booleano, Data, Ora, DataOra

>[!note] Vincoli
>
>Per modellare il mondo reale abbiamo bisogno di definire dei vincoli sui tipi, ad esempio un vote di un esame è compreso tra 18 e 30.
>
>Esempi di vincoli:
>- `cfu : Intero >= 0`
>- `media : Reale < 31`
>- `voto : 18..30` (si utilizza soltanto per intervalli di interi)
>
>![[Screenshot 2025-03-04 at 19.03.17.png|600]]

---
## Dati Enumerativo (enumerazione)

Quando l’insieme dei possibili valori di un attributo è finito e piccolo, possiamo usare un **tipo di dato enumerativo**, che definisce esplicitamente e completamente l’insieme dei valori possibili per l’attributo. Ad esempio:

$$
\text{\{Africa,\; America,\; Antartide,\; Asia,\; Europa,\; Oceania\}}
$$


**Rappresentazione:** il dominio enumerativo si definisce con le graffe e dentro scriviamo tutte le costanti enumerative.

>[!example] Esempio
>
>![[Screenshot 2025-03-05 at 08.23.35.png|900]]
>
>È anche possibile creare il tipo di dato genere:
>
>![[Pasted image 20250305082728.png|700]]
>
>>Mi scuso per l'esempio poco inclusivo ma è stato fatto dal professore. 

---
## Dati Composti (record)

UML consente all’analista di definire anche **tipi di dato composti** da più campi: **tipi record**.

![[Pasted image 20250305082908.png|1000]]

>***oss:*** Si definisce con le tonde e dentro ci inseriamo i vari dati e come rappresentarli

---
## Vincoli di molteplicità sugli attributi

Anche gli attributi di classe e associazione possono avere vincoli di molteplicità, dove di default abbiamo `[1..1]` (quando non inseriamo nessun vincolo).

>[!example] Eempio
>
>- Ogni studente ha associato esattamente un nome e un genere
>- Ogni studente ha associato **uno o più** indirizzi email
>- Ogni studente ha associato **al più un** indirizzo
> 
>![[Pasted image 20250305083304.png|900]]  

>***oss:*** sono gli unici vincoli che si definiscono con le quadre, tutti gli altri sono con le graffe (il prof ha detto che il signo UML era ubriaco)

---
## Vincoli di Identificazione

I vincoli di identificazione ci permettono di definire gli attributi che identificano univocamente gli oggetti di una determinata classe.

Questo impone a due differenti istanze di una classe, di non poter avere uno o più attributi `id` coincidenti.

>[!example] Esempio
>
>![[Pasted image 20250305150554.png|250]]
>
>In questo caso non possono esistere due persone che hanno lo stesso codice fiscale (`{id1}`), ed in oltre non possono esistere due persone che uguale tripla di nome, cognome e data di nascita (`{id2}`).

>[!danger] Più vincoli di identificazione su lo stesso attributo
>
>È possibile assegnare più vincoli di identificazione allo stesso attributo.
>
>Fai esempio Studente con:
>- `cf : stringa {id1} {id2}`
>- `nome : stringa {id1}`
>- `cognome : stringa {id1}`
>- `matricola : stringa {id2}`

>[!note] Vincolo di Intensificazione sul Ruolo
>
>Un vincolo di identificazione di classe può coinvolgere anche ruoli della classe.
>
>![[Pasted image 20250306082014.png|500]]
>
>In questo esempio non possono esistere due studenti con la stessa matricola nella stessa università
>
>>***oss:*** questo vale soltanto se il vincolo di molteplicità di studente sul link è `[1..1]`.

>[!danger] Vincoli di moltoplicita e identificazione
>
>Un vincolo di identificazione di classe può coinvolgere soltanto **attributi** con molteplicità `[1..1]` e/o **ruoli** **della classe** con molteplicità `1..1`.
