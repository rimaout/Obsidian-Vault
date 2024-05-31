---
created: 2024-03-08
type: Programming Note
programming language: "[[Java MOC]]"
related:
  - "[[Java OOP]]"
completed: false
updated: 2024-05-27T13:29
---
---

>[!info] Index
>1. 

---

>[!question] Perché utilizziamo le parole chiave public e private?
>- Per nascondere le informazioni (“information hiding”) all’utente

Il **processo che nasconde i dettagli realizzativi**, prende il nome di **incapsulamento**, che permette di utilizzare determinate classi senza conoscere il loro funzionamento attraverso un interfaccia publica

>[!note] Definition
>- Dettagli realizzativi: campi e implementazione
>- Interfaccia pubblica: metodi pubblici

Si semplifica e modularizza il lavoro di sviluppo assumendo un certo funzionamento a “scatola nera”
- Non è necessario sapere tutto, soprattutto molti inutili dettagli
- L’incapsulamento facilita il lavoro di gruppo e l’aggiornamento del codice (maintenance)
- Aiuta a rilevare errori: in presenza di moltissime classi, un certo errore si verifica solo in una determinata classe per cui ci si può concentrare su di essa

---