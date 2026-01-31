---
created: 2026-01-31T13:32
updated: 2026-01-31T13:32
---
Academic Year: 2022-2023
Class: [[Programmazione Calcolatori (Class)]]
Created: May 9, 2023
Tag: [[C MOC]]
Type: #Uni/Lecture 

---
# Union 
La Union è una variabile che può contenere un elemento ma il tipo di elemento può cambiare 

## Sintassi
```c
// Definizione per creazione di un tipo Union
// Union che possa memorizare o un carattere, o un intero, o un float
union nome_union{
	char c_val;
	int i_val;
	float f_val;
} 
```

```c
// Definizione per una singola variabile
// Union che possa memorizare o un carattere, o un intero, o un float
union {
	char c_val;
	int i_val;
	float f_val;
} u  // u è una variabile di tipo union;
```

## Size di una union
La direzione in memoria della union è la dimensione del del tipo di elemento più grande dichiarato nella union 

## Esempio Utilizzo 
```c
u.i_val = 10; // assegno un valore intero alla variabile i_val
printf("%d", u.i_val); // stampo il valore intero
printf("%c", u.c_val); // provo a stampare il valore carattere 
// c_val non definito (non è detto che sia stampato correttamente)

u.c_val = 'a'; // assegno un valore carattere alla variabile c_val
printf("%c", u.c_val); // stampo il valore carattere
printf("%d", u.i_val); // provo a stampare il valore intero
// i_val non definito (non è detto che sia stampato correttamente)
```
