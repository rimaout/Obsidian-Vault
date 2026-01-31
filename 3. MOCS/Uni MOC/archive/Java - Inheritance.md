---
type: Uni Note
class: "[[Metodologie di Programmazione (class)]]"
academic year: 2024/2025
related:
  - "[[Java MOC]]"
completed: true
created: 2025-01-27T20:03
updated: 2026-01-31T13:32
---
L'ereditarietà è uno dei meccanismi fondamentali della programmazione orientata agli oggetti, che consente di ridurre la ridondanza del codice permettendo alle classi figlie di ereditare campi e i metodi della classe madre.

Il livello di ereditarietà dei membri (campi e metodi) può essere controllato attraverso i [[Java - Access Modifier|modificatori di accessibilità]].

![[Pasted image 20250127202018.png|700]]

### Object (extends implicito)

In Java tutte le classi estendono implicitamente la classe `Object`. Ciò significa che ogni classe, anche se non è stata definita esplicitamente come una sottoclasse di `Object`, eredita comunque le proprietà e i metodi di `Object`

I metodi di object più comunemente utilizzato sono;
- `getClass()`--> restituisce una rappresentazione stringa dell'oggetto
- `toString()` --> restituisce la classe dell'oggetto
- `hashCode()` --> restituisce un codice hash per l'oggetto
- `equals()` --> confronta l'oggetto con un altro oggetto per determinare se sono uguali

>[!warning] Ovveride
>
>Questi metodi possono essere sovrascritti dalle classi figlie per fornire un comportamento personalizzato, ecco qui alcuni re-implementazioni comuni di questi metodi:
>
>- [[Java - HashCode & Equals Methods]]
>- [[Java - Clone Method]]