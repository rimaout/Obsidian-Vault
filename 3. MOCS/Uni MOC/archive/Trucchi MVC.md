---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2024-10-27T11:06
updated: 2024-11-14T12:25
---
>[!abstract] Related
>- 

---

1. Il controller non deve mai modificare direttamente nel model, quindi non può usare dei setter del tipo:, 
- `playingModel.setPause(false)`
- ma deve dare tipo: `playingModel.unpauseGame()`

2. Controller poi deve usare observer observable per comunicare quando aggiornare i model e le view e quando fare i draw.

3. In oltre observer observable può essere utilizzato per spostare informazioni tra view e model. esempio view to controller to model
	- quando possibile sarebbe sempre meglio evitarlo infatti nella realtà c'è sempre una dipendenza tra view e model
	- Esempio per gli stati sarebbe meglio usare un timer invece di usare la view per dire quando una animazione è finta

5. L'audio manager deve essere e tutte le cose riguardati l'audio devono essere nella view

