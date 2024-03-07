Academic Year: 2022-2023
Class: [[Programmazione Calcolatori (Class)]]
Created: March 23, 2023
Tag: [[C MOC]]
Type: #Uni/Lecture 

---
# [[C malloc Function]]
La funzione `malloc()` in C serve per allocare dinamicamente la memoria durante l'esecuzione del programma.

- permette di richiedere una porzione di memoria di dimensioni specifiche e restituisce un puntatore a tale area di memoria.

- **input:** intero che e quivale al numero di byte
- **esecuzione:** cerca uno spazio in memoria sufficentemente grande
- **output:** indirizzo di memoria del primo di questi byte (pointer)
	- in caso d errore (esempio assenza di meoria libera) restituisce un puntatore nullo 

la memoria occupata dalla funzione malloc viene riallocata soltanto alla fine del programma o all'infocazione della funzione `free`
>[!warning] Nota:
>Puntatore nullo = `NULL`

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int n;
    printf("Inserisci la dimensione dell'array: ");
    scanf("%d", &n);
    int *arr = (int*) malloc(n * sizeof(int));
    if (arr == NULL) {
        printf("Errore: memoria non disponibile\n");
        exit(1);
    }
    for (int i = 0; i < n; i++) {
        arr[i] = i;
    }
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    free(arr);
    return 0;
}
```
In questo esempio, l'utente inserisce la dimensione dell'array `arr` che viene poi allocato dinamicamente con `malloc()`. Successivamente, l'array viene inizializzato con valori crescenti e stampato a schermo. Infine, la memoria allocata viene liberata con `free()`.

**Riallocazione della memoria:**
- la memoria occupata dalla funzione malloc viene riallocata soltanto alla fine del programma o manualmente atraverso l'invocazzione della funzione `free`.

# [[C free Function]]
la memoria allocata con `malloc()` deve essere liberata manualmente con la funzione `free()` quando non serve più, altrimenti si rischia di incorrere in memory leak.