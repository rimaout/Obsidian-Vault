---
type: Uni Note
class: "[[Basi di Dati 1 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-03-12T14:36
updated: 2026-01-31T13:32
---
## Introduzione

Una classe ha un nome, degli attributi e delle operazioni, esse definiscono il comportamento della classe e differentemente dagli attributi non sono statici.

![[Screenshot 2025-03-12 at 14.41.43.png|600]]

Un operazione è una *proprietà* il cui valore è calcolato a partire dai valori dell’oggetto che la invoca ad altri oggetti ad esso correlati, un operazione può anche cambiare lo stato di un oggetto. Quando un operazione modifica un oggetto, si dice che provoca degli **effetti collaterali**.

>[!warning] Come decidere se un operazione è di classe
>
>L'operazioni di classe di base dovrebbero sempre ritornare un dato, che viene collegato dall'operazione. Solitamente possono essere viste come dei campi (dati) che però per essere ottenuti devono essere calcolati.
>
>Ad esempio:
>- [X] `NumeroEsamiSostenuti()` è un operazione di calasse.
>- [ ] `PartecipaEsame()` non è un operazione di classe, dato che non ritorna nessun dato.

## Struttura

Una operazione della classe `C` indica che su ogni oggetto (istanza) della classe `C` si può eseguire un calcolo per:
- calcolare un valore a partire da altri dati e operazioni.
- effettuare cambiamenti di stato dell’oggetto (cioè per modificare le sue proprietà), dei link in cui è coinvolto e/o degli oggetti a questo collegati.

>***oss:*** Il diagramma delle classi non definisce cosa calcolano le operazioni, né se e come modificano i dati. Ogni classe del diagramma con operazioni andrà affiancata da un documento di specifica che entra nel dettaglio.

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

## Specifica

In UML quindi vengono definite le operazioni, parametri e tipo di ritorno, ma non viene esplicitato in maniera formale cosa queste operazioni devono calcolare.

La descrizione logica-formale di ciò che le operazioni devono fare (non come), viene data in un [[|documento di specifica]] separato.