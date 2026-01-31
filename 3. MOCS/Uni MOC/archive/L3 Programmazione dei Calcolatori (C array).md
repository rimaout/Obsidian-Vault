---
created: 2026-01-31T13:32
updated: 2026-01-31T13:32
---
Academic Year: 2022-2023
Class: [[Programmazione Calcolatori (Class)]]
Created: March 22, 2023
Tag: [[C MOC]]
Type: #Uni/Lecture 

---
**Dati scalari in c:**
- char 
- float 
- double
- int
- array

# [[C Arrays]] int

```c
int a[10];
```
- Array di dieci elemnti imenti non ancora definiti
- vuoto

```c
int b[] = {0,10,20,30,40};
int c[5] = {0,10,20,30,40}; 
```
 - indicano la `b` e `c` sono uguali 

```c
int d[10] = {1,2,3,4,5,6};
// d = 1,2,3,4,5,6,0,0,0,0
```
- se non completiamo un array, gli elementi non itilizzati verranno posti come 0

**Creare un array di lunghezza 100 composto solo da 0**
```c
int d[100] = {0};
```

## Indice di un [[C Arrays]]

Sostituzione di un elemnto:
```c
int e[5] = {1,2,3,4};
e[5] = 5;
```

Stampare uno o più elementi:
```c
int f[5] = {1,2,3,4,5};

printf("%d, %d, %d, %d, %d",f[0], f[1], f[2], f[3], f[4]);
```

## [[C sizeof Function]]

La funzione `sizeof()` ritorna il peso in byte di un tipo di dato o variabile:

```c
int g[10];
int x = sizeof(g)
```

```c
sizeof(char));   // Output: 1
sizeof(int));    // Output: 4
sizeof(float));  // Output: 4
sizeof(double)); // Output: 8
```

### Calcolo della lunghezza di un array

```c
int g[5] = {1,2,3,4,5};

int len_h = sizeof(h)/sizeof(int); // Output: 5
```
- con questo metodo possiamo calcolare la lunghezza (il numero di elementi di un array)

## Tempo di accesso ad un array 
- è costante 
- ovvero accedere a qualsiasi elemento richiede tempo costante (indipendentemente dalla posizione)
