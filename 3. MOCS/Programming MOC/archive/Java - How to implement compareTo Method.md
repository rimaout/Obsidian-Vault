---
type: Programming Note
programming language: 
related: 
completed: false
created: 2025-01-26T17:16
updated: 2025-01-26T17:17
---


in questo confronterò la difficoltà

```java
@Override
public int compareTo(Recepi o) {
	if (this.difficulty > o.difficulty)
		return 1
	
	if (this.difficulty < o.difficulty)
		return -1
	
	else return 0
}
```
