---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: true
created: 2025-01-26T13:52
updated: 2026-01-31T13:32
---
Il risultato dell'utilizzo della keyword `final` dipende dal tipo di elemento su cui la si sta applicando:

>[!note] Classi Final
>
>Una classe dichiarata come `final` ***non può essere estesa***. Ciò implica che nessuna classe può ereditare una classe final, questo è utili per impedire che una classe venga modificata attraverso l’[[Java - Inheritance|ereditarietà]].

>[!note] Metodi Final
>
> Un metodo dichiarato come `final` ***non può essere sovrascritto*** attraverso un `@override` da nessuna sotto classe.

>[!note] Campi Final
>
>Una campi dichiarato come `final` ***non può essere modificato dopo la sua assegnazione***, questo significa che deve essere inizializzato al momento della dichiarazione o nel costruttore della classe.
