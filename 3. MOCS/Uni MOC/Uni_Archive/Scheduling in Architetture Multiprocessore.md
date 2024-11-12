---
type: Uni Note
class:
  - "[[Sistemi Operativi 1 (class)]]"
academic year: 2024/2025
related: "[[Scheduling]]"
completed: true
created: 2024-11-07T11:56
updated: 2024-11-07T12:30
---
>[!abstract] Related
>- [[Scheduling]]
>- [[Sistemi Operativi 1 (class)]]

---
## Introduzione 

Esistono tre tipi di sistemi multiprocessore:
- **Cluster:** Ogni processore ha la sua RAM e una rete locale.
- **Processori Specializzati:** Ad esempio ogni I/O ha un suo processore
- **Multiprocessore e/o multicore:** Condividono la RAM e c’è un solo sistema operativo che controlla tutto. 

In questa sezione ci concentriamo sui sistemi **Multiprocessore e/o multicore** dove a differenza dei sistemi mono-processore visti fino ad ora capire se un processo è _ready_ e si deve anche decidere su quale processore eseguire il processo.

Il processo di scegliere su quale processore eseguire un processo è chiamato assegnamento:
- [[#Assegnamento Statico]]
- [[#Assegnamento Dinamico]]

---
### Assegnamento Statico
- Quando un processo viene creato gli viene assegnato un processore e per tutta la sua durata andrà sempre in esecuzione su di lui.
- Possiamo utilizzare uno scheduler per ogni processore
- Come vantaggio abbiamo che è semplice da realizzare e poco **overhead** (lavoro aggiuntivo)
- Come svantaggio abbiamo che qualche processore può rimanere in idle, causato appunto dal fatto che scegliamo sempre lo stesso processore per ogni processo

---
### Assegnamento Dinamico

- Nel corso della sua esistenza un processo può essere spostato su un altro processore
- È più complesso da realizzare

>[!warning] Processi di sistema
>Questo metodo può andare bene sui processi utente, ma per quelli del sistema operativo?
>
>**Metodo Statico:**
>Questi potrebbero essere eseguiti sullo stesso processore in modo da essere realizzabile più facilmente, però potrebbe causare bottleneck dato che ha più carico rispetto agli altri e inoltre se quel processore va in errore o smette di funzionare, si blocca tutto il sistema operativo.
>
>**Metodo Dinamico:**
>È più ragionevole quindi eseguire il sistema operativo su più processori anche se causa un maggiore overhead dato dal fatto che il S.O. è eseguito in continuazione.
