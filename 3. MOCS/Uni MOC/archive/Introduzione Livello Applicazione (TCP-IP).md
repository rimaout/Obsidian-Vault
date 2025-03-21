---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: true
created: 2025-03-17T09:10
updated: 2025-03-17T19:05
---
## Introduzione

Il livello applicazione fornisce *servizi all’utente*. Due utenti possono immaginare che tra di essi esista un *canale logico bidirezionale* attraverso il quale si possono inviare messaggi. La comunicazione reale avviene attraverso più livelli e più dispositivi, e vari canali fisici.

![[Screenshot 2025-03-17 at 09.19.03.png|500]]

>[!note] Servizi non Standard
>
>Aggiungere o eliminare protocolli dal livello applicazione è relativamente facile perché non comporta modifiche agli altri livelli.
>
>**Protocolli Standard** - Protocolli di livello applicazione standardizzati e documentati dagli enti responsabili della gestione di Internet (es. HTTP). Tutti i protocolli standard sono costituiti da una coppia di programmi che interagiscono con l’utente e con il livello di trasporto per fornire uno specifico servizio.
>
>**Protocolli non Standard** - E’ possibile creare un’applicazione non standard scrivendo due programmi che forniscono servizi agli utenti, facendo uso dei servizi di trasporto, ***non è necessario chiedere autorizzazioni***.
## Creare applicazioni di Rete

Quando si crea un applicativo sulla rete si deve prendere in considerazione che:
- Verrà eseguito su diversi sistemi terminali
- Comunicano attraverso la rete

Si dovrà scegliere:
- il **tipo di architettura** client-server o peer-to-peer.
- il come **comunicano i processi** dell'applicazione.
- Tipi di **servizi di rete** di cui usufruirà l'applicazione.

### Paradigma Architettare Client Server

Il ruolo delle due entità è totalmente differente: non è possibile eseguire un client come programma server e viceversa.

>[!note] Client
>- Richiedente il servizio
>- In esecuzione solo quando è necessario il servizio
>- Numerosi client che richiedono il servizi

>[!note] Server
>- fornitore di servizi
>- Sempre in esecuzione, in attesa di richieste dal client
>- Numero limitato di processi server pronti a offrire uno specifico servizio

![[Pasted image 20250317093557.png|700]]

>[!danger] Svantaggi
>
>- Carico di comunicazione risulta concentrato sul server (che deve essere molto potente)
>- Server farm per creare un potente server virtuale
>- Costi di gestione per offrire servizio

---
## Protocolli Livello Applicazione

- [[World Wide Web e HTTP]]
- [[Cookie]]
- [[Web Caching]]

![[Pasted image 20250313142228.png|700]]

