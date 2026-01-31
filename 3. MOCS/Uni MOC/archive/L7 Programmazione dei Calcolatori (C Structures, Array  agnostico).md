---
created: 2026-01-31T13:32
updated: 2026-01-31T13:32
---
Academic Year: 2022-2023
Class: [[Programmazione Calcolatori (Class)]]
Created: April 5, 2023
Tag: [[C MOC]]
Type: #Uni/Lecture 

---
1. Correzione esercizio per casa: costruire funzione che trova la posizione degli spazzi vuoti di una stringa.
2. funzione [[C realloc Function]]
3. implementazione funzione pop (usando realloc)
4. implementazione di una lista stile python 

# implementazione lista in c stile python
- array non conterrà più gli elementi ma sarà composto da puntatori che puntano agli elementi
- utilizziamo **\*void**  come puntatore in modo da poter puntare a dati di tipo diverso (e utilizzare [[Python Data Types|Casting]] per accedere ai giusto tipo di puntatore)

**Struttura:**
- Utilizziamo una normale lista i cui elementi puntano a delle strutture (objects) che contengono 2 informazioni:
	- 1. Il tipo di elemento (type) es: type = 'i' (intero)
	- 2. L' elemento vero e proprio sotto dorma di puntatore

```c
struct object {
	char type; // 'i', 'c' ed 's' per int, char e stringa
	void *pointer; // puntatore all' elemnto vero e proprio
};
```

