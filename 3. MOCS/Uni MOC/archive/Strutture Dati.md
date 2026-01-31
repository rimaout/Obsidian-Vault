---
created: 2024-04-11
type: Uni Note
class:
  - "[[Algoritmi 1 (class)]]"
academic year: 2023/2024
related:
completed: true
updated: 2026-01-31T13:32
---
---

>[!info] Index
>1. [[#Tipi]]
>2. [[#Definizione]]
>	- [[#Insiemi Omogenei e Disomogenei]]
>	- [[#Insiemi Dinamici e Statici]]

>[!info] Related
>- [[Algoritmi 1 (class)]]

---
## Tipi

- [[Array (Struttura Dati)]] 🟢
- [[Linked List (Struttura Dati)]] 🟡 (aggiungere codice)
- [[Pile (Struttura Dati)]] 🟢
- [[Code (Struttura Dati)]] 🟢
- [[Heap (Struttura Dati)]] 🟡 (da finire)
- [[Alberi (Struttura Dati)]] 🟢
- [[Alberi Binari (Struttura Dati)|Alberi Binari (Struttura Dati):]] 
	- [[Memorizzazione tramite puntatori (Alberi Binari)|Memorizzazione tramite puntatori]] 🟢
	- [[Rappresentazione posizionale (Alberi Binari)|Rappresentazione posizionale]] 🟢
	- [[Rappresentazione tramite vettore dei padri (Alberi Binari)|Rappresentazione tramite vettore dei padri]] 

>[!warning] Ogni struttura dati compie due tipi di operazioni:
>**Operazioni di interrogazione:**
>- `Search(S,x)`: recuperare valore associato alla chiave `x` in `S`
>- `Min(S)`: recuperare il minimo valore in `S`
>- `Max(S)`: recuperare il massimo valore in `S`
>
>**Operazioni di manipolazione:**
>- `Insert(S,x):` inserire un elemento di valore `x` in `S`
>- `Delete(S,x):` rimuovere un elemento di valore `x` in `S`

---
## Definizione

>[!info] Struttura di base
>Una struttura dati è composta da:
>- un modo sistematico di **organizzare i dati**
>- un insieme di **operatori** che permettono di **manipolare** la struttura

>[!info] Tipi
>Le strutture dati possono essere:
>- **Omogenee** o **Disomogenee** (rispetto ai dati contenuti).
>- **Statiche** o **Dinamiche** (a seconda che possano o meno variare la dimensione nel tempo)

### Insiemi Omogenei e Disomogenei 

>[!info] Omogenei 
>Insiemi omogenei possono contenere un solo tipo di dati. Esempio un array di interi.

>[!info] Disomogenei
>Insiemi disomogenei possono contenere più tipi di dati. Esempio le liste di python.

### Insiemi Dinamici e Statici

>[!info] Statici 
>Un insieme statico è una struttura dati omogenei in cui la dimensione è fissa e deve essere specificata al momento della creazione.
>- Non possono cambiare di dimensione durante l'esecuzione del programma
>- Sono generalmente più efficienti in termini di spazio e accesso.
>- Sono utili quando si conosce a priori la dimensione massima dell'insieme e si vuole evitare l'overhead di gestire una dimensione variabile

>[!info] Dinamici
>Un insieme dinamico è una struttura dati in cui la dimensione può cambiare dinamicamente durante l'esecuzione del programma.
>- Possono crescere o ridursi automaticamente per ospitare un numero variabile di elementi senza dover specificare una dimensione massima in anticipo.
>- Sono utili quando la dimensione dell'insieme è incerta o può cambiare nel tempo.

---
