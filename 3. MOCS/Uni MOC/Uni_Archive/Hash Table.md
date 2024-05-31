---
created: 2024-05-13T12:53
type: Uni Note
class: 
academic year: 2023/2024
related: 
completed: false
updated: 2024-05-27T13:29
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

