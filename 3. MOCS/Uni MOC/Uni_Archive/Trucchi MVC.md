---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2024-10-27T11:06
updated: 2024-10-27T11:11
---
>[!abstract] Index
>1. 

>[!abstract] Related
>- 

>[!danger] TLDR

---

Il controller non deve mai modificare direttamente nel model, quindi non può usare dei setter del tipo:, 
- `playingModel.setPause(false)`
- ma deve dare tipo: `playingModel.unpauseGame()`

Controller poi deve usare observer observable per comunicare quando aggiornare i model e le view e quando fare i draw.

In oltre observer observable può essere utilizzato per spostare infomazioni tra view e model.

