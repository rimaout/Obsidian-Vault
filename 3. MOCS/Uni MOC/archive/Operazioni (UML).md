---
type: Uni Note
class: "[[Basi di Dati 1 (class)]]"
academic year: 2024/2025
related: 
completed: true
created: 2025-03-12T14:36
updated: 2025-03-17T19:29
---
## Introduzione

Una classe UML può definire anche proprietà dinamiche, che si chiamano operazioni (in java metodi).

Le proprietà dinamiche sono valori calcolati ogni volta che servono, a partire dai valori di altre proprietà o attributi.

## Operazioni di Classe

Una operazione della classe `C` indica che su ogni oggetto (istanza) della classe `C` si può eseguire un calcolo per:
- calcolare un valore a partire da altri dati e operazioni
- effettuare cambiamenti di stato dell’oggetto (cioè per modificare le sue proprietà), dei link in cui è coinvolto e/o degli oggetti a questo collegati

>***oss:*** Il diagramma delle classi non definisce cosa calcolano le operazioni, né se e come modificano i dati. Ogni classe del diagramma con operazioni andrà affiancata da un documento di specifica che entra nel dettaglio.

![[Screenshot 2025-03-12 at 14.41.43.png|450]]

>[!note] Sintassi
>
>```java
>nome_operazione(argomenti) : tipo_ritorno
>```
>- ***argomenti*** è una lista di elementi della forma `nome_argomento : tipo_argomento`
>- ***tipo_ritorno*** è il tipo del valore restituito dall’operazione
>
>Una operazione di classe può essere invocata *solo* su un oggetto della classe.

>[!note] Ereditarietà
>
>Il meccanismo dell’ereditarietà si applica anche alle operazioni di classe, ad esempio:
>
>![[Screenshot 2025-03-17 at 19.27.52.png|500]]
>
>In questo caso è possibile chiamare l'operazione `madia_fino_A(...)` anche su studente straniero.
