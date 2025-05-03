---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-04-29T14:27
updated: 2025-04-29T14:56
---
Questo protocollo sul i dea di **link state**, ovvero il costo associato al link (collegamento).

**Link State Database (LSBD):**

Il link state database mantiene la *mappa completa della rete*, e *ogni nodo ne mantiene una copia*. 

>[!note] Rappresentazione
>
>É rappresentato attraverso una matrice dove `M[x][y]` contiene il costo del collegamento tra il nodo `x` e il nodo `y`.
>
>![[Pasted image 20250429145002.png|700]]

>[!note] Creazione
>
>Ogni nodo della rete deve innanzitutto conoscere i propri vicini e i costi dei collegamenti verso di loro, per fare ciò:
>- ogni nodo invia un messaggio di `hello` a tutti i suoi vicini
>- ogni nodo riceve gli `hello` dei vicini e crea la lista dei vicini chiamata **LS Packet (LSP)*** contenente tuple `(vicino, costo)`.
>
>Ogni nodo esegue un *flooding*, ovvero invia la lista LSP a tutti i sui vicini


