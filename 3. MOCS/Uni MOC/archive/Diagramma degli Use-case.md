---
type: Uni Note
class: "[[Basi di Dati 2 (class)]]"
academic year: 2024/2025
related:
completed: true
created: 2025-03-22T12:37
updated: 2026-01-31T13:32
---
## Introduzione

I diagrammi degli use-case modellano le **funzionalità** che il sistema deve realizzare, in termini di **use-case** (scenari di utilizzo), si basa su due concetti centrali:

>[!note] Use-case
>Cattura un **insieme omogeneo di funzionalità** accedute da un **gruppo omogeneo di utenti**. Tipicamente coinvolge concetti rappresentati da più classi e associazioni del diagramma delle classi.

>[!note] Attore
>
>Ruolo che un utente (umano o sistema esterno) gioca interagendo con il sistema, dove:
>
>- Lo stesso utente può essere rappresentato da più attori (può giocare più ruoli).
>- Più utenti possono essere rappresentati dallo stesso attore.

### Grafo

Un diagramma UML degli use-case non è altro che un grafo in cui:

>[!note] Nodi
>I nodi rappresentano **attori** e **gli use-case**.

>[!note] Archi
>Gli archi rappresentano:
>- la possibilità per un attore di invocare uno use-case
>- la possibilità per uno use-case di invocare un altro use-case
>- la generalizzazione tra attori e tra use-case

## Associazione

Un associazione modella la possibilità di accesso, da parte di un attore, alle funzionalità di uno use-case.

![[Pasted image 20250319141945.png|500]]

>[!warning] Attenzione
>
>Il diagramma degli use case **non modella le classi**, in questo esempio l’esistenza dell’attore `Utente` non implica l’esistenza della classe Utente nel diagramma delle classi.
>- Avremo la classe Utente **solo se** il sistema deve rappresentare **dati** sugli utenti.

>[!example] Esempio
>
>Il sistema deve permettere agli **studenti** di iscriversi, via web, ai corsi offerti. La **segreteria** deve poter assegnare i docenti ai singoli corsi. I **docenti** devono poter inserire i risultati dei test degli studenti: tali test sono somministrati agli studenti utilizzando il sistema.
>
>![[Pasted image 20250322121440.png|800]]
>

## Dipendenze

>[!note] Inclusione
>
>Alcune funzionalità dello use-case A hanno bisogno di usare alcune funzionalità dello use-case B
>
>---
>
>**Esempio:**
>
>1. I docenti possono creare e valutare i test degli studenti.
>2. Gli studenti possono rispondere ai test.
>3. Test e le risposte degli studenti vanno memorizzati nel sistema.
>   
>![[Pasted image 20250322122229.png|450]]

>[!note] Estensione
>
>Alcune funzionalità dello use-case A, solo in alcuni casi particolari, sono estese con le funzionalità dello use-case B.
>
>---
>
>**Esempio:**
>
>1. Gli studenti possono iscriversi a corsi
>2. Durante il processo di iscrizione, gli studenti possono optare per il pagamento online.
>
>![[Pasted image 20250322122417.png|450]]

## Generalizzazione

>[!note] Generalizzazione tra use-case
>
>Alcune funzionalità dello use-case A, solo in alcuni casi particolari, sono rimpiazzate con le funzionalità dello use-case B.
>
>
>
>1. Gli studenti devono potersi identificare
>2. L’identificazione online avviene tramite password
>3. Registrazione delle presenze ai corsi avviene tramite scansione impronta digitale dal lettore del tortello
>
>---
>**Esempio:**
>
>![[Pasted image 20250322123252.png|450]]

>[!note] Generalizzazione tra attori
>
>L’attore `B` può fare le veci dell’attore `A`, e ne eredita tutte le associazioni.
>
>---
>**Esempio:**
>
>I manager possono fare le veci della `Segreteria`, ed accedere a tutti gli use-case accessibili dalla `Segreteria`.
>
>![[Pasted image 20250322123537.png|450]]
> 
>***Attenzione:***  Il diagramma non implica che esistano le classi `Segreteria` e `Manager` nel diagramma delle classi, né tantomeno che la classe `Manager` sia una sottoclasse di `Segreteria`.

## Conclusione 

Il diagramma degli use-case è molto semplice, e dà solo una visione di alto livello di:
- quali attori possono usare il sistema
- quali macro-funzionalità sono accessibili ai diversi attori

Si tratta di un diagramma facilmente comprensibile anche al committente, per questo:
- Il diagramma **non** definisce le singole operazioni all’interno di ogni use-case
- Ogni use-case del diagramma andrà affiancato da un [[Specifica Use-Case]] che entra nel dettaglio