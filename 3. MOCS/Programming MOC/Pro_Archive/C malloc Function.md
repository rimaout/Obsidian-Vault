---
Created: 2022-03-22
Type: Programming Note
Programming Language: "[[C MOC]]"
Related:
  - "[[C Embedded  Functions]]"
  - "[[C free Function]]"
  - "[[C realloc Function]]"
Completed: true
---
---

La funzione `malloc()` ha la seguente firma:

```c
void* malloc(size);
```

- `size`: è un parametro che rappresenta la dimensione in byte della memoria da allocare.

- `return`: la funzione restituisce un puntatore di tipo `void*` alla memoria allocata. 
- Se la memoria non può essere allocata, la funzione restituisce `NULL`.

Ad esempio, se si vuole allocare dinamicamente un array di 10 interi, si può utilizzare la funzione `malloc()` in questo modo:
```c
int* arr = (int*) malloc(10 * sizeof(int));
```
In questo caso, la funzione `malloc()` alloca 10 * sizeof(int) byte di memoria e restituisce un puntatore di tipo `void*` che viene poi convertito in un puntatore di tipo `int*`. Questo puntatore può essere utilizzato per accedere all'array allocato dinamicamente.

## Computational Cost
- constant O(1)

**Esempio:**
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

---
È importante **liberare la memoria allocata** con `malloc()` quando non serve più, altrimenti si rischia di incorrere in memory leak. 

La funzione `free()` viene utilizzata per liberare la memoria allocata con `malloc()`.
[[C free Function]]

---


