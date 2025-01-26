---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: true
created: 2025-01-26T14:06
updated: 2025-01-26T14:41
---

Il risultato dell'utilizzo della keyword `static` varia in base al tipo di elemento su cui la si sta applicando:

>[!note] Classe Statica
>
>Non è possibile definire `static`una classe standard, ma è possibile utilizzare il modificatore static su una classe dichiarata dentro un altra classe.
>
>Infatti le classi interne sono chiamate in due modi specifici:
>- **Inner Class:** classe interna *non statica*
>- **Nested Class:** classe interna *statica*
>
>Le differenza sono che:
>
>Un `inner class` (non statica):
>- non può essere istanziata senza creare un istanza della sua classe esterna
>- ha acceso ai membri (campi e metodi) della classe esterna.
>
>Una `nested class` (statica):
>- può essere istanziata senza istanziare la sua classe esterna
>- ha acceso soltanto ai membri statici della esterna

>[!note] Metodo Statico
>
>I metodi statici appartengono alla classe e non ad una istanza specifica della classe, questo implica che:
>- possono essere invocati anche utilizzando il nome della classe e non si un istanza
>- possono chiamare ed utilizzare soltanto metodi e campi statici

>[!note] Campo Statico
>
>I campi statici appartengono alla classe e non ad una istanza specifica della classe, questo implica che:
>
>- sono accessibili anche attraverso il nome della classe e non solo attraverso un istanza
>- esiste una sola allocazione del dato che è condivisa tra tutte le istanza
