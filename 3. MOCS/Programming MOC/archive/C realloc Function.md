---
created: 2023-03-22
type: Programming Note
programming language: "[[C MOC]]"
related:
  - "[[C Embedded  Functions]]"
  - "[[C malloc Function]]"
  - "[[C free Function]]"
completed: true
updated: 2024-05-27T13:29
---
---
## Index
1. [[#Description]]
2. [[#Syntax]]
3. [[#Return Value]]
4. [[#Computational Cost]]
5. [[#Example]]

---
## Description

The C library function void ``realloc(void \*ptr, size)`` attempts to resize the memory block pointed to by **ptr** that was previously allocated with a call to **malloc** or **calloc**.

If **there isn’t enough memory space** in the previous position, the function may move the memory block to a new location (whose address is returned by the function).

---
## Syntax
```c
void *realloc(void *ptr, size)
```

- **ptr** − This is the pointer to a memory block previously allocated with malloc, calloc or realloc to be reallocated. If this is NULL, a new block is allocated and a pointer to it is returned by the function.

- **size** − This is the new size for the memory block, in bytes. If it is 0 and ptr points to an existing block of memory, the memory block pointed by ptr is deallocated and a NULL pointer is returned.

---
## Return Value
- This function returns a pointer to the newly allocated memory
**oss:** non c'è bisogno di fare il controllo per vedere s l'operazione è andata a buon fine (la [[C malloc Function]] ne ha bisogno)

---
## Computational Cost
- Constant O(1)
- Linear O(n), if needs to reallocate the memory (worsts case)

---
## Example
**realloc:**
```c

array_int array_int_append( array_int v, int e ){
	// aggiunge un elemento in coda all'array di interi
	
	if (v.n == v.c){ // Controllo se l'array è pieno 
			v.a = realloc(v.a, (2*v.c+1)*sizeof(int)); 
			v.c = 2*v.c+1;
		}

	v.a[v.n] = e; // inserimento dell'elemento
	v.n++; // incremento il numero di elementi
	
	return v;
	
}
```

**Same example but using malloc:**
```c

array_int array_int_append( array_int v, int e ){
	int i;
	int *a;
	
	if (  v.n == v.c ){
		a = malloc((2*v.c+1)*sizeof(int));
		if (a == NULL)
			return v;
		
		for(i = 0; i < v.n; i++){
			a[i] = v.a[i]; 
		}
		v.c = 2*v.c+1;
		free(v.a);
		v.a = a;
	}
	v.a[v.n] = e;
	v.n++;
	
	return v;
```

---