---
type: Uni Note
class:
  - "[[Sistemi Operativi 2 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-10-03T19:41
updated: 2026-01-31T13:32
---
## Shell

La bash è un interprete di comandi, aspetta la richiesta di esecuzione da parte dell'utente di un programma. È estremamente utile perché permette di effettuare tutte le possibili operazioni effettuabili sul sistema, senza utilizzare nessuna interfaccia grafica.

La shell mentre attende che l'utente scriva un “commando”, mostra un **prompt** che solitamente ha questa struttura: `nomeutente@nomemacchina:~cammino$`; dove `cammino` è il path dalla directory home dell'utente alla directory attuale.

## Utenti

Durante l’installazione di linux è necessario specificare (almeno) un utente (utente principale).

Ogni utente appartiene almeno ad un **gruppo**:
- Automaticamente è creato un gruppo con lo stesso nome dell’utente principale
- Esistono molti gruppi definiti per scopi "amministrativi"

>[!note] Creazione Utenti
>
>Per creare un’utente è possibile utilizzare il comando `adduser nuovoutente`, per aggiungere il nuovo utente ad un gruppo possiamo utilizzare `adduser nuovoutente gruppo`.

>[!note] sudo e sudoers
>
>Nelle distribuzioni della famiglia Ubuntu l’utente principale e’ un `sudoer`, appartiene al gruppo predefinito `sudo`.
>
>Il comando `sudo` (super user do) prende come input un altro comando che però verra eseguiva con privilegi da super utente (root).
>
>Il comando sudo richiederà la password dell'utente che lo ha chiamato. 

>[!note] Cambiare Utente
>
>- Per passare a un'altra shell di root (chiederà la password di root): `su -`
>- Per eseguire shell come un altro utente (chiederà la password dell'utente target): `su - username`
