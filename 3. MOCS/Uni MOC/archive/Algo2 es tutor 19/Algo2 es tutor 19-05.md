---
type: Uni Note
class: 
academic year: 2024/2025
related: 
completed: false
created: 2025-05-19T09:53
updated: 2025-05-19T10:20
---

![[Screenshot 2025-05-19 at 09.28.05.png|700]]


---

![[Screenshot 2025-05-19 at 09.52.18.png|700]]

```python
def es(S, i=0):
	if i == len(S)-1:
		if S[i] != 0: # S[i] è una lettera valida
			return 1
		else:
			return 0

	output = 0
	
	if S[i] != 0: 
		output = 1 + es(S, i+=1) # S[i] è una lettera valida

	if i+1 < len(S) and S[i]<=2 and S[i+1]<=26:
		output = 1+ es(S, i+=2) # S[i]*10 + S[i+1] è una lettera valida
			
	return output
```