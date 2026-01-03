---
type: Programming Note
programming language: "[[Java MOC]]"
related:
  - "[[Metodologie di Programmazione (class)]]"
  - "[[Software Design Pattern]]"
completed: false
created: 2024-07-12T18:03
updated: 2024-07-12T20:24
---
>[!abstract] Index
>1. 

>[!abstract] Related
>- [[Software Design Pattern]]
>- [[Metodologie di Programmazione (class)]]
>- [[Java MOC]]

---
## Introduzione

**Decorator** è un pattern strutturale che consente di aggiungere nuovi comportamenti a un oggetto senza modificare la sua implementazione, inserendolo all'interno di speciali oggetti wrapper che contengono i nuovi comportamenti.

>[!note] Problema
> Imaginiamo di dover creare una libreria che permette di inviare messaggi di notifica attraverso altre applicazioni. Per fare ciò, inizialmente creiamo una classe `notifier` e delle sottoclassi che implementano metodi per inviare notifiche attraverso alcune specifiche applicazioni. 
>
>![[Pasted image 20240712194209.png|400]]
>
>Imaginiamo ora di dover implementare un modo per inviare la stessa notifica simultaneamente con più applicazioni.vPer fare ciò, potrebbe sembrare sensato, creare una nuova sottoclasse di `notifier` per ogni combinazione di applicazioni.
>
>![[Pasted image 20240712194507.png|500]]
>
>Naturalmente questa non è una soluzione ottimale, in quando il codice sarebbe poco leggibile, e aggiungere un nuovo metodo di notifica richiederebbe la creazione di tantissime nuove classi.

>[!note] Soluzione
>Crea un oggetto decoratore che avvolge l'oggetto originale. L'oggetto decoratore contiene un riferimento all'oggetto originale e aggiunge nuove funzionalità. L'oggetto decoratore conforma alla stessa interfaccia dell'oggetto originale, quindi può essere utilizzato come sostituto diretto.

**Componenti chiave:**

1. **Componente:** L'oggetto originale a cui vuoi aggiungere nuove funzionalità.
2. **Decoratore:** L'oggetto che avvolge il componente e aggiunge nuove funzionalità.
3. **Decoratore concreto:** Una implementazione specifica del decoratore che aggiunge una funzionalità specifica.

**Come funziona:**

1. Il client richiede un oggetto con comportamento aggiuntivo.
2. Viene creato l'oggetto decoratore, che avvolge l'oggetto componente originale.
3. L'oggetto decoratore aggiunge nuove funzionalità all'oggetto componente.
4. Il client interagisce con l'oggetto decoratore, che inoltra le richieste all'oggetto componente e aggiunge il suo proprio comportamento.

**Vantaggi:**

- Consente di aggiungere nuove funzionalità a un oggetto senza modificare la sua implementazione.
- Abilita l'aggiunta di multiple funzionalità a un oggetto mediante l'impilamento di più decorator.
- Fornisce un modo flessibile per estendere il comportamento di un oggetto senza cambiare la sua implementazione sottostante.

---

>[!info] Sources
>- https://www.youtube.com/watch?v=v6tpISNjHf8
