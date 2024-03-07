Academic Year: 2022-2023
Class: [[Programmazione Calcolatori (Class)]]
Created: March 12, 2023
Tag: [[C MOC]]
Type: #Uni/Lecture 

---
**Info utili precedenti:** [[L33 Programmazione dei Calcolatori (C Linked Lists)]]

## Node Search
```c
node *search(linked_list L, int pos){
	node *p = L.a;
	int i = 0;
	
	while( p != NULL && i < pos ){ // se p è NULL, la lista è finita
		p = p->next;
		i++;
	}

return p;
}
```
**Costo:** O(n), lineare dipende dall'input pos

## inserire nuovo elemento in una lista frammentata 
- cambiare puntatore next con posizione del nuovo elemento successivo 
- creare nuovo elemento con head e nest
- cambiare head dell' elemento d’eccessivo al nuovo elemento inserito ![[IMG_EE39F4E0B00D-1.jpeg]]
**oss:** questo meccanismo funziona per l inserimento di un nuovo elemento in tutte le posizioni tranne che nella prima

```c
linked_list insert(linked_list L, int pos, float e){
	
	if(pos > 0 && pos <= L.size){
		node *p = malloc(sizeof(node));
		node *q = search(L, pos-1);
		
		p->data = e;
		p->next = q->next;
		q->next = p;
		L.size++;
		
	} else if(pos == 0) {
		L = in0(L, e);
	}
	return L
}
```
**Costo:** O(n), dipende dalla funzione search (lineare) il resto ha tutto costo costante

### inserimento elemento in posizione 0
```c
linked_list in0(linked_list L, float e){
	node *p = malloc(sizeof(node));
	
	p->data = e;
	p->next = NULL;
	L.a = p;
	L.size++;
	
	return L;
// crea nodo con valore e e lo inserisce in testa alla lista
}
```

## Cancellazione di un elemnto 
Cancella l'elemento in una specifica posizione di una lista e restituisce la nuova lista
![[IMG_E4DFAB5C5E20-1 2.jpeg]]

```c


```


### Cancellazione di elemento iniziale

![[IMG_90DA64294FD7-1.jpeg]]

```c

```

### Cancellazione di una lista con elemento stringa

![[IMG_B7A2844D5110-1.jpeg]]

```c

```

## Int main input

- l'int main può prendere come input ...
**es:**

```c

```