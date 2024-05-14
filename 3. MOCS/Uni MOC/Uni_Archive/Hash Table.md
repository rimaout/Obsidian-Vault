---
Created: ""
Type: Uni Note
Class: 
Academic Year: 2023/2024
Related: 
Completed: false
---
---

>[!abstract] Index
>1. 

>[!abstract] Related
>- 

---

```python
def hash(s): 
	t=0
	for x in S:
		t += ord(x)

	return t%20
```

non è una buona funzione hash perché:
- è costosa (ogni volta che devo cercare/salvare  un elemento viene utilizzata)
- è non omogenea (infatti dipende dalla lingua)

