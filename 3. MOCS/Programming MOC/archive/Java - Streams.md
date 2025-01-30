---
type: Programming Note
programming language: 
related: 
completed: false
created: 2024-06-17T18:21
updated: 2025-01-30T15:41
---
## Introduzione 

Un `Stream` in Java può essere visto come una sequenza di dati. Un `Stream` non memorizza dati e, in questo senso, non è una struttura dati che memorizza elementi. Piuttosto, rappresenta una sequenza di elementi e funzioni di supporto che possono essere utilizzate per eseguire operazioni su quegli elementi.

##### Concetti Chiave

>**🔥 Nota:** Al contrario delle Collection, uno Stream non memorizza né modifica i dati della sorgente, ma opera su di essi

>[!note] Stram Pipeline
>Una pipeline di stream è una sequenza di operazioni di stream, composta da: 
>- **Sorgente:** che può essere una [[Java - Collections|collezione]], un [[Java - Arrays|array]], un generatore di numeri, ecc.
>- **Operazioni intermedie:** che trasformano un stream in un altro stream.
>- Un **operazione terminale:** (che produce un risultato o un effetto collaterale, come `count` o `forEach`).

>[!note] Operazioni intermedie vs Operazioni terminali
>Le **operazioni intermedie** restituiscono un altro stream su cui continuare a lavorare.
>
>come filter e map restituiscono un nuovo stream. Sono sempre lazy, eseguendo un'operazione su un elemento dello stream solo quando necessario.
>
>Le **operazioni terminali** come forEach, count, collect, ecc., producono un risultato o un effetto collaterale e terminano la pipeline.
>[!note] Stream sequenziali vs Stream paralleli
>Un stream sequenziale ha un unico elemento corrente, elaborato in modo indipendente dagli altri. 
>
>Un stream parallelo è in grado di suddividere il suo lavoro in più parti, elaborando più elementi contemporaneamente.


---
