---
Created: 2003-11-21
Type: Programming Note
Programming Language: "[[Python MOC]]"
Related: 
Completed:
---
---
# Index

---
## Mutable data types as default parameter
It's highly suggested to not use mutable objects as default functions parameters, in fact they are prone to hard to identify errors

``` python
def add_to(num, target=[]):
	target.append(num)
	return target

add_to(1) # expected_Output: [1] # real_Output: [1]
add_to(2) # expected_Output: [2] # real_Output: [1,2]
add_to(3) # expected_Output: [3] # real_Output: [1,2,3]

```

**How resolve this problem:**
``` python
def add_to(num, target=None):
	if target is None:
		target = []
	
	target.append(num)
	return target

add_to(1) # expected_Output: [1] # real_Output: [1]
add_to(2) # expected_Output: [2] # real_Output: [2]
add_to(3) # expected_Output: [3] # real_Output: [3]
```

---